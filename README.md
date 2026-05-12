🏦 Banking System in C

A console-based banking application written in C that supports deposits, withdrawals, and balance checks with persistent file storage — balance survives between program runs.

📋 Table of Contents

Features
Concepts Covered
Project Structure
How It Works
Getting Started
Usage
Sample Output


Features
FeatureDescriptionDepositAdd funds to the accountWithdrawDeduct funds with balance validationBalance CheckDisplay current account balancePersistenceBalance is saved to balance.dat and restored on next run

Concepts Covered

switch-case — routes menu choices to the correct operation
while loop — keeps the menu running until the user exits
File Handling — fopen, fscanf, fprintf, fclose for reading and writing balance to disk


Project Structure
banking-system/
├── banking_system.c   # Main source file
├── balance.dat        # Auto-generated at runtime — stores current balance
└── README.md

balance.dat is created automatically on the first deposit. You can add it to .gitignore if you don't want to track it.


How It Works

Program Start
     │
     ▼
Read balance.dat  ──── (if file missing, balance = 0.0)
     │
     ▼
Display Menu  ◄──────────────────────────┐
     │                                   │
     ▼                                   │
switch(choice)                           │
  ├── 1: deposit()  ── update balance ──►│
  ├── 2: withdraw() ── validate + update►│
  ├── 3: checkBalance() ── read + print ►│
  ├── 4: exit()
  └── default: invalid message ─────────►┘
File persistence flow:

Every deposit() and withdraw() calls writeBalance() which overwrites balance.dat with the new value using fprintf.
Every operation starts with readBalance() which uses fscanf to load the current value.
If balance.dat does not exist (first run), readBalance() returns 0.0f.


Getting Started
Prerequisites

GCC compiler (or any C99-compatible compiler)

Compile
bashgcc banking_system.c -o banking
Run
bash# Linux / macOS
./banking

# Windows
banking.exe

Usage
After running, you will see:
==============================
    SIMPLE BANKING SYSTEM
==============================

--- MENU ---
1. Deposit
2. Withdraw
3. Check Balance
4. Exit
Enter your choice:
Enter 1, 2, 3, or 4 and follow the prompts.

Sample Output
--- MENU ---
1. Deposit
Enter your choice: 1
Enter deposit amount: 5000
Deposited: Rs 5000.00
New Balance: Rs 5000.00

--- MENU ---
Enter your choice: 2
Enter withdrawal amount: 1500
Withdrawn: Rs 1500.00
Remaining Balance: Rs 3500.00

--- MENU ---
Enter your choice: 3
Current Balance: Rs 3500.00

Notes

Amounts must be greater than 0. Negative or zero values are rejected.
Withdrawal is blocked if the amount exceeds the current balance.
Balance is stored as a float with 2 decimal places.
