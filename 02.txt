#include <iostream>
#include <cstring>

using namespace std;

class Account
{
	private:
	string Name;
	long long int CNIC;
	int balance;

	public:

	Account(): Name(""), CNIC(0), balance(0)
	{
        
	}
	
	friend ostream & operator << (ostream &out, const Account &A); 
    friend istream & operator >> (istream &in,  Account &A); 

	/*void CreateAccount(string &n, long long int &c, int &accounts)
	{
		if(CNIC != 0)
		{
			cout << "ERROR! An account with that name has already been registered!";
		}
		else
		{
			Name = n;
			CNIC = c;
			balance = 0;
			cout << "Account has been created successfully! - Account Number: " << accounts << endl;
			accounts++;
		}
	}*/
	void DepositCash(int &cash)
	{
		balance+= cash;
		cout << "[SYSTEM]: " << cash << " has been deposited to your account." << "New Balance: " << balance << endl;
	}
	void WithdrawCash(int &cash)
	{
		if(balance < cash)
			cout << "ERROR! You have insufficient balance." << endl;
		else
		{
			balance  -= cash;
			cout << "You have withdrawn "<< cash << ". Remaining Balance: "<< balance << endl;
		}
	}
	string getname()
	{
		return Name;
	}
	int getcnic()
	{
		return CNIC;
	}
	int getbalance()
	{
		return balance;
	}
	void setname(const string &n)
	{
		Name = n;
	}
	void setcnic(const long long int &c)
	{
		CNIC = c;
	}
};

ostream & operator << (ostream &out, Account &A) 
{ 
	cout << "Name: "<< A.getname() << endl;
	cout << "CNIC: "<< A.getcnic() << endl;
	cout << "Balance: " << A.getbalance() << endl;
    return out; 
} 
  
istream & operator >> (istream &in,  Account &A) 
{ 
    
	cout << "Enter account name:";
	in >> A.Name;
	cout << "Enter CNIC:";
	in >> A.CNIC;
    return in; 
} 


int main()
{
	int count = 0;
	int input;
	bool error = 0;
	int acc, cash;
	string name;
	Account A[100];

    Main_Menu:
	cout << "Select an option" << endl;
	cout << "1. Create Account" << endl;
	cout << "2. Deposit Cash" << endl;
	cout << "3. Withdraw Cash" << endl;
	cout << "4. Show Accounts" << endl;
	cout << "5. Account Details" << endl;
	cout << "\n[INPUT]: ";
	cin >> input;
	cout << endl;
	switch(input)
	{
		case 1:
		cin >> A[count];
		for(int i = 0; i < count; i++)
		{
			if(A[i].getcnic() == A[count].getcnic())
			{
				cout << "ERROR! An account has already been created with that cnic.";
				A[count].setname("");
				A[count].setcnic(0);
				error = 1;
				break;
			}
		}
		if(error == 0)
		{
			cout << "Account has been created successfully! - Account Number: " << count << endl;
			count++;
		}
		error = 0;
		break;

		case 2:
		
		cout << "Enter account number: ";
		cin >> acc;
		cout << "Enter amount to deposit: ";
		cin >> cash;
		A[acc].DepositCash(cash);
		break;

		case 3:


		cout << "Enter account number: ";
		cin >> acc;
		cout << "Enter amount to withdraw: ";
		cin >> cash;
		A[acc].WithdrawCash(cash);
		break;

		case 4:
		
		cout << endl;
		cout << "------------------------" << endl;
		cout << "\tAccounts" << endl;
		cout << "------------------------" << endl;
		for(int i=0; i < count; i++)
		{
			cout << i << ". " << A[i].getname() << " [" << A[i].getcnic() << "]" << " - Balance: " << A[i].getbalance() << endl;
	    }
		break;

		case 5:

		cout << "Enter account number: ";
		cin >> acc;
		cout << "Account Details:" << endl;
		cout << "Account Number:" << acc << endl;
		cout << A[acc];

	}

	cout << "\n\n";
	goto Main_Menu;
	return 0;
}




