# GitHub-Practice
This is my first Git repository.
#include <iostream>  
#include <string>  
#include <vector>  

using namespace std;  

// Base class for account details  
class Account {  
protected:  
    string accountHolder;  
    int accountNumber;  
    double balance;  

public:  
    Account(string holder, int number, double bal = 0.0)  
        : accountHolder(holder), accountNumber(number), balance(bal) {}  

    void deposit(double amount) {  
        balance += amount;  
        cout << "Deposited: $" << amount << " | New Balance: $" << balance << endl;  
    }  

    void withdraw(double amount) {  
        if (balance >= amount) {  
            balance -= amount;  
            cout << "Withdrew: $" << amount << " | New Balance: $" << balance << endl;  
        } else {  
            cout << "Insufficient balance!" << endl;  
        }  
    }  

    double getBalance() const {  
        return balance;  
    }  

    void displayAccountInfo() const {  
        cout << "Account Holder: " << accountHolder << endl;  
        cout << "Account Number: " << accountNumber << endl;  
        cout << "Balance: $" << balance << endl;  
    }  
};  

// Derived class for Savings Account  
class SavingsAccount : public Account {  
public:  
    SavingsAccount(string holder, int number, double bal = 0.0)  
        : Account(holder, number, bal) {}  

    void displayAccountType() const {  
        cout << "Account Type: Savings Account" << endl;  
    }  
};  

// Derived class for Current Account  
class CurrentAccount : public Account {  
public:  
    CurrentAccount(string holder, int number, double bal = 0.0)  
        : Account(holder, number, bal) {}  

    void displayAccountType() const {  
        cout << "Account Type: Current Account" << endl;  
    }  
};  

// Bank class to manage accounts  
class Bank {  
private:  
    vector<SavingsAccount> savingsAccounts;  
    vector<CurrentAccount> currentAccounts;  

public:  
    void addSavingsAccount(string holder, int number, double bal = 0.0) {  
        savingsAccounts.emplace_back(holder, number, bal);  
    }  

    void addCurrentAccount(string holder, int number, double bal = 0.0) {  
        currentAccounts.emplace_back(holder, number, bal);  
    }  

    void displayAllAccounts() {  
        cout << "\nSavings Accounts:\n";  
        for (const auto& account : savingsAccounts) {  
            account.displayAccountInfo();  
            account.displayAccountType();  
            cout << endl;  
        }  

        cout << "\nCurrent Accounts:\n";  
        for (const auto& account : currentAccounts) {  
            account.displayAccountInfo();  
            account.displayAccountType();  
            cout << endl;  
        }  
    }  
};  

int main() {  
    Bank myBank;  

    myBank.addSavingsAccount("Alice Smith", 101, 500.0);  
    myBank.addCurrentAccount("Bob Johnson", 202, 1000.0);  

    // Displaying account details  
    myBank.displayAllAccounts();  

    // Performing transactions  
    myBank.savingsAccounts[0].deposit(200);  
    myBank.savingsAccounts[0].withdraw(150);  
    
    myBank.currentAccounts[0].deposit(500);  
    myBank.currentAccounts[0].withdraw(200);  

    return 0;  
}