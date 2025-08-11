# Banking-Account-Simulation
Simulate basic bank operation using java oop

import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

class Account {
    private String accountNumber;
    private String accountHolder;
    private double balance;
    private List<String> transactionHistory;

    
    public Account(String accountNumber, String accountHolder, double initialBalance) {
        this.accountNumber = accountNumber;
        this.accountHolder = accountHolder;
        this.balance = initialBalance;
        this.transactionHistory = new ArrayList<>();
        transactionHistory.add("Account created with balance: " + initialBalance);
    }

    
    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
            transactionHistory.add("Deposited: " + amount + " | Balance: " + balance);
            System.out.println(" Deposit successful! Current Balance: " + balance);
        } else {
            System.out.println(" Invalid deposit amount!");
        }
    }

    
    public void withdraw(double amount) {
        if (amount > 0 && amount <= balance) {
            balance -= amount;
            transactionHistory.add("Withdrew: " + amount + " | Balance: " + balance);
            System.out.println(" Withdrawal successful! Current Balance: " + balance);
        } else {
            System.out.println(" Invalid amount or insufficient balance!");
        }
    }

    
    public void checkBalance() {
        System.out.println(" Current Balance: " + balance);
    }

    
    public void showTransactionHistory() {
        System.out.println("\n Transaction History for " + accountHolder + ":");
        for (String record : transactionHistory) {
            System.out.println(record);
        }
    }
}


public class BankSimulation {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        
        System.out.print("Enter account number: ");
        String accNumber = sc.nextLine();

        System.out.print("Enter account holder name: ");
        String accHolder = sc.nextLine();

        System.out.print("Enter initial balance: ");
        double initialBalance = sc.nextDouble();

        Account account = new Account(accNumber, accHolder, initialBalance);

        
        int choice;
        do {
            System.out.println("\n---  Bank Menu ---");
            System.out.println("1. Deposit");
            System.out.println("2. Withdraw");
            System.out.println("3. Check Balance");
            System.out.println("4. View Transaction History");
            System.out.println("5. Exit");
            System.out.print("Enter your choice: ");
            choice = sc.nextInt();

            switch (choice) {
                case 1:
                    System.out.print("Enter deposit amount: ");
                    double depositAmt = sc.nextDouble();
                    account.deposit(depositAmt);
                    break;

                case 2:
                    System.out.print("Enter withdrawal amount: ");
                    double withdrawAmt = sc.nextDouble();
                    account.withdraw(withdrawAmt);
                    break;

                case 3:
                    account.checkBalance();
                    break;

                case 4:
                    account.showTransactionHistory();
                    break;

                case 5:
                    System.out.println(" Exiting... Thank you for banking with us!");
                    break;

                default:
                    System.out.println(" Invalid choice! Please try again.");
            }
        } while (choice != 5);

        sc.close();
    }
}
