# Banking-System
A code for a banking system in Java
public interface Account {
void deposit(double amount);
void withdraw(double amount);
double getBalance();
}
public abstract class AbstractAccount {
protected String accountNumber;
protected String accountHolder;
protected double balance;
public AbstractAccount(String accountNumber,String accountHolder, double balance) {
	 this.accountNumber = accountNumber;
	 this.accountHolder = accountHolder;
	 this.balance = balance;
	 }
public void deposit(double amount) {
	 if(amount > 0) {
		 balance += amount;
		 System.out.println("Deposited $ " + amount + "New balance: $ " + balance);
	 }
		 else {
			 System.out.println("Deposit amount must be positive.");
			
		 }
	 }
public double getBalance() {
	 return balance;
}
public abstract void withdraw (double amount);
public void displayAccountInfo() {
	 System.out.println("Account Number:  " + accountNumber);
	 System.out.println("Account holder:  " + accountHolder);
	 System.out.println("Balance:  $ " + balance);
	
}
}
public class BankingSystem {
	public static void main(String[] args) {
		SavingsAccount savings = new SavingsAccount("TR1234566", "MIMIDOO SARAH CHEN", 200.0, 3.0);
		CheckingAccount checking = new CheckingAccount("TR567489290", "MSUGHTER ISAAC CHEN",450.0,677.0);
		
		//for depositing and withdrawing
		System.out.println("Savings Account transactions :");
		savings.displayAccountInfo();
		savings.deposit(500);
		savings.withdraw(300);
		savings.addInterest();
		System.out.println("Final Balance: $" + savings.getBalance());
		
		//For checking the transaction
		System.out.println("\nChecking Account Transaction: ");
		checking.displayAccountInfo();
		checking.deposit(300);
		checking.deposit(1200);
		System.out.println("Final balance : "+ checking.getBalance);
		
	}
}
public class CheckingAccount extends AbstractAccount {
   //to limit their transactions so that user will not withdraw over
	private double overdraftLimit;
	
	public CheckingAccount(String accountNumber, String accountHolder, double balance) {
	super(accountNumber, accountHolder, balance);
	this.overdraftLimit = overdraftLimit;
	}
	public void withdraw(double amount) {
		if (amount > 0 && balance + overdraftLimit >= amount) {
			balance -= amount;
			System.out.println("Withdrew $" + amount + ".New balance: $" + balance);
		}
			else {
				System.out.println("Exceeded overdraft limit or invalid amount for withdrawal.");
			}
		}
	}
public class SavingsAccount extends AbstractAccount {
private double interestRate;
public SavingsAccount(String accountNumber, String accountHolder, double balance, double interestRate) {
	 super(accountNumber, accountHolder, balance);
	 this.interestRate = interestRate;
}
public void withdraw(double amount) {
	 if(amount > 0 && amount <= balance) {
		 balance-= amount;
		 System.out.println("Withdrew $ :" + amount + ".New balance: $ " + balance);
	 }
	 else {
		 System.out.println("Insufficient balance or invalid amount for withdrawak.");
	 }
	 }
public void addInterest() {
	 double interest = balance * interestRate / 100;
	 balance += interest;
	 System.out.println("Interest added. New balance: $ " + balance);
}
}
	
