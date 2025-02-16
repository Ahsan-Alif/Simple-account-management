import java.util.Scanner;

class BankAccount {
    String accountHolder;
    int accountNumber;
    double balance;

    public BankAccount(String accountHolder, int accountNumber, double balance) {
        this.accountHolder = accountHolder;
        this.accountNumber = accountNumber;
        this.balance = balance;
    }

    public int getAccountNumber() {
        return accountNumber;
    }

    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
            System.out.println("Deposited: $" + amount);
            System.out.println("New Balance: $" + balance);
        } else {
            System.out.println("Invalid deposit amount.");
        }
    }

    public void withdraw(double amount) {
        if (amount > 0 && amount <= balance) {
            balance -= amount;
            System.out.println("Withdrawn: $" + amount);
            System.out.println("New Balance: $" + balance);
        } else {
            System.out.println("Invalid withdrawal amount or insufficient funds.");
        }
    }

    public void displayAccountInfo() {
        System.out.println("\nAccount Holder: " + accountHolder);
        System.out.println("Account Number: " + accountNumber);
        System.out.println("Current Balance: $" + balance);
    }
}

public class BankAccount1 {
    private static final String ADMIN_PASSWORD = "ahsan123";

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("Enter Admin Password: ");
        String password = scanner.nextLine();

        if (!password.equals(ADMIN_PASSWORD)) {
            System.out.println("Incorrect password. Access denied.");
            return;
        }

        System.out.println("\nAdmin Access Granted\n");

        System.out.print("Enter the number of accounts: ");
        int numAccounts = scanner.nextInt();
        scanner.nextLine(); // Consume newline

        BankAccount[] accounts = new BankAccount[numAccounts];

        for (int i = 0; i < numAccounts; i++) {
            System.out.println("\nEnter details for Account " + (i + 1) + ":");
            System.out.print("Enter Account Holder Name: ");
            String name = scanner.nextLine();
            System.out.print("Enter Account Number: ");
            int accountNumber = scanner.nextInt();
            System.out.print("Enter Initial Balance: ");
            double balance = scanner.nextDouble();
            scanner.nextLine(); // Consume newline

            accounts[i] = new BankAccount(name, accountNumber, balance);
        }

        while (true) {
            System.out.println("\nChoose an option:");
            System.out.println("1. Deposit");
            System.out.println("2. Withdraw");
            System.out.println("3. Display Account Info");
            System.out.println("4. Exit");
            System.out.print("Enter your choice: ");
            int choice = scanner.nextInt();

            if (choice == 4) {
                System.out.println("Exiting system. Goodbye!");
                break;
            }

            System.out.print("Enter Account Number: ");
            int accountNumber = scanner.nextInt();
            BankAccount selectedAccount = null;

            for (int i = 0; i < accounts.length; i++) {
                if (accounts[i].getAccountNumber() == accountNumber) {
                    selectedAccount = accounts[i];
                    break;
                }
            }
            

            if (selectedAccount == null) {
                System.out.println("Invalid Account Number.");
                continue;
            }

            switch (choice) {
                case 1:
                    System.out.print("Enter deposit amount: ");
                    double depositAmount = scanner.nextDouble();
                    selectedAccount.deposit(depositAmount);
                    break;
                case 2:
                    System.out.print("Enter withdrawal amount: ");
                    double withdrawAmount = scanner.nextDouble();
                    selectedAccount.withdraw(withdrawAmount);
                    break;
                case 3:
                    selectedAccount.displayAccountInfo();
                    break;
                default:
                    System.out.println("Invalid choice. Please try again.");
            }
        }

        scanner.close();
    }
}
