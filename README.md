# atm-system
 import java.util.*;

// 1. BANK
class Bank {
    private int bankID;
    private String bankName;
    private String branch;
    private String address;
    private List<ATM> atms;

    public Bank(int bankID, String bankName, String branch, String address) {
        this.bankID = bankID;
        this.bankName = bankName;
        this.branch = branch;
        this.address = address;
        this.atms = new ArrayList<>();
    }

    public void addATM(ATM atm) {
        atms.add(atm);
        System.out.println("ATM added: " + atm.getAtmID());
    }

    public void removeATM(ATM atm) {
        atms.remove(atm);
        System.out.println("ATM removed: " + atm.getAtmID());
    }

    public void updateBankDetails(String name, String branch, String address) {
        this.bankName = name;
        this.branch = branch;
        this.address = address;
    }

    public void processTransaction(Transaction transaction) {
        transaction.createTransaction();
    }

    public String getBankName() {
        return bankName;
    }
}

// 2. ATM
class ATM {
    private int atmID;
    private String location;
    private String bankName;
    private float availableCash;

    public ATM(int atmID, String location, String bankName, float availableCash) {
        this.atmID = atmID;
        this.location = location;
        this.bankName = bankName;
        this.availableCash = availableCash;
    }

    public boolean verifyCard(Card card) {
        return card.validateCard();
    }

    public void dispenseCash(float amount) {
        if (availableCash >= amount) {
            availableCash -= amount;
            System.out.println("Dispensed: " + amount);
        } else {
            System.out.println("Insufficient ATM cash.");
        }
    }

    public void displayBalance(Account account) {
        System.out.println("Balance: " + account.getBalance());
    }

    public void printReceipt(Receipt receipt) {
        receipt.printReceipt();
    }

    public int getAtmID() {
        return atmID;
    }
}

// 3. ACCOUNT
class Account {
    private int accountID;
    private String accountHolderName;
    private String accountNumber;
    private String accountType;
    private float balance;

    public Account(int accountID, String name, String number, String type, float balance) {
        this.accountID = accountID;
        this.accountHolderName = name;
        this.accountNumber = number;
        this.accountType = type;
        this.balance = balance;
    }

    public void debit(float amount) {
        if (balance >= amount) {
            balance -= amount;
            System.out.println("Debited: " + amount);
        } else {
            System.out.println("Insufficient balance.");
        }
    }

    public void credit(float amount) {
        balance += amount;
        System.out.println("Credited: " + amount);
    }

    public float getBalance() {
        return balance;
    }

    public void updateAccountDetails(String name, String type) {
        this.accountHolderName = name;
        this.accountType = type;
    }

    public int getAccountID() {
        return accountID;
    }

    public String getAccountHolderName() {
        return accountHolderName;
    }
}

// 4. TRANSACTION
class Transaction {
    private int transactionID;
    private int accountID;
    private float amount;
    private String transactionType;
    private Date transactionDate;
    private String status;

    public Transaction(int transactionID, int accountID, float amount, String type) {
        this.transactionID = transactionID;
        this.accountID = accountID;
        this.amount = amount;
        this.transactionType = type;
        this.transactionDate = new Date();
        this.status = "Pending";
    }

    public void createTransaction() {
        this.status = "Completed";
        System.out.println("Transaction successful: " + transactionType + " of " + amount);
    }

    public void cancelTransaction() {
        this.status = "Cancelled";
        System.out.println("Transaction cancelled.");
    }

    public void getTransactionDetails() {
        System.out.println("ID: " + transactionID + ", Amount: " + amount + ", Type: " + transactionType + ", Status: " + status);
    }

    public void updateTransactionDetails(String newStatus) {
        this.status = newStatus;
    }

    public int getTransactionID() {
        return transactionID;
    }

    public float getAmount() {
        return amount;
    }

    public Date getTransactionDate() {
        return transactionDate;
    }

    public String getStatus() {
        return status;
    }
}

// 5. CARD
class Card {
    private String cardNumber;
    private Date expiryDate;
    private String cardHolderName;
    private String bankName;
    private String pin;
    private int accountID;
    private boolean blocked;

    public Card(String cardNumber, Date expiryDate, String cardHolderName, String bankName, String pin, int accountID) {
        this.cardNumber = cardNumber;
        this.expiryDate = expiryDate;
        this.cardHolderName = cardHolderName;
        this.bankName = bankName;
        this.pin = pin;
        this.accountID = accountID;
        this.blocked = false;
    }

    public boolean validateCard() {
        return !blocked && expiryDate.after(new Date());
    }

    public boolean checkPin(String inputPin) {
        return this.pin.equals(inputPin);
    }

    public void updatePin(String newPin) {
        this.pin = newPin;
        System.out.println("PIN updated successfully.");
    }

    public void blockCard() {
        blocked = true;
        System.out.println("Card has been blocked.");
    }

    public int getAccountID() {
        return accountID;
    }

    public String getCardHolderName() {
        return cardHolderName;
    }
}

// 6. RECEIPT
class Receipt {
    private int receiptID;
    private int transactionID;
    private Date date;
    private float amount;
    private int atmID;

    public Receipt(int receiptID, int transactionID, float amount, int atmID) {
        this.receiptID = receiptID;
        this.transactionID = transactionID;
        this.amount = amount;
        this.atmID = atmID;
        this.date = new Date();
    }

    public void generateReceipt() {
        System.out.println("Receipt generated.");
    }

    public void printReceipt() {
        System.out.println("Receipt ID: " + receiptID + ", Transaction ID: " + transactionID +
                ", Amount: " + amount + ", Date: " + date + ", ATM ID: " + atmID);
    }

    public void emailReceipt(String email) {
        System.out.println("Receipt emailed to: " + email);
    }
}

// 7. USER
class User {
    private int userID;
    private String name;
    private String address;
    private String phone;
    private String email;

    public User(int userID, String name, String address, String phone, String email) {
        this.userID = userID;
        this.name = name;
        this.address = address;
        this.phone = phone;
        this.email = email;
    }

    public void authenticate() {
        System.out.println("User authenticated.");
    }

    public void viewAccountDetails(Account account) {
        System.out.println("Account Holder: " + account.getAccountHolderName() + ", Balance: " + account.getBalance());
    }

    public void requestCardReplacement() {
        System.out.println("Card replacement requested.");
    }

    public void updateUserInfo(String name, String phone, String email) {
        this.name = name;
        this.phone = phone;
        this.email = email;
    }
}

// MAIN
public class ATMSystem {
    public static void main(String[] args) {
        Bank bank = new Bank(1, "Smart Bank", "Main", "Dhaka");
        ATM atm = new ATM(101, "Banani", bank.getBankName(), 50000);
        bank.addATM(atm);

        Account account = new Account(5001, "Azim", "SB123456", "Savings", 10000);
        User user = new User(1001, "Azim", "Dhaka", "017xxxxxxxx", "azim@example.com");

        Card card = new Card("1234-5678-9012-3456", new GregorianCalendar(2030, Calendar.JANUARY, 1).getTime(),
                "Azim", bank.getBankName(), "1234", account.getAccountID());

        if (atm.verifyCard(card) && card.checkPin("1234")) {
            Transaction transaction = new Transaction(9001, account.getAccountID(), 2000, "Withdrawal");
            bank.processTransaction(transaction);
            account.debit(2000);
            atm.dispenseCash(2000);

            Receipt receipt = new Receipt(3001, transaction.getTransactionID(), transaction.getAmount(), atm.getAtmID());
            receipt.generateReceipt();
            atm.printReceipt(receipt);
        } else {
            System.out.println("Card verification failed or incorrect PIN.");
        }
    }
}
