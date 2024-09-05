import os
import pickle

# File names
EXPENSE_FILE = "expenses.pkl"
BUDGET_FILE = "budgets.pkl"

# Constants
MAX_DESCRIPTION = 100
MAX_CATEGORY = 50

class Expense:
    def __init__(self, description, amount):
        self.description = description
        self.amount = amount

class Budget:
    def __init__(self, category, limit):
        self.category = category
        self.limit = limit
        self.spent = 0

def authenticate(username, password):
    stored_username = "user"
    stored_password = "pass"
    return username == stored_username and password == stored_password

def add_expense():
    description = input("Enter expense description: ")
    amount = float(input("Enter expense amount: "))
    expense = Expense(description, amount)
    
    with open(EXPENSE_FILE, "ab") as file:
        pickle.dump(expense, file)
    
    print("Expense added successfully.")

def list_expenses():
    if not os.path.exists(EXPENSE_FILE):
        print("No expenses recorded.")
        return

    with open(EXPENSE_FILE, "rb") as file:
        print("Expenses:")
        while True:
            try:
                expense = pickle.load(file)
                print(f"Description: {expense.description}, Amount: {expense.amount:.2f}")
            except EOFError:
                break

def set_budget():
    category = input("Enter budget category: ")
    limit = float(input("Enter budget limit: "))
    budget = Budget(category, limit)
    
    with open(BUDGET_FILE, "ab") as file:
        pickle.dump(budget, file)
    
    print("Budget set successfully.")

def update_budget(category, amount):
    if not os.path.exists(BUDGET_FILE):
        print("No budgets recorded.")
        return

    updated = False
    budgets = []
    
    with open(BUDGET_FILE, "rb") as file:
        while True:
            try:
                budget = pickle.load(file)
                if budget.category == category:
                    budget.spent += amount
                    updated = True
                budgets.append(budget)
            except EOFError:
                break
    
    if updated:
        with open(BUDGET_FILE, "wb") as file:
            for budget in budgets:
                pickle.dump(budget, file)
    else:
        print("Category not found.")

def list_budgets():
    if not os.path.exists(BUDGET_FILE):
        print("No budgets recorded.")
        return

    with open(BUDGET_FILE, "rb") as file:
        print("Budgets:")
        while True:
            try:
                budget = pickle.load(file)
                print(f"Category: {budget.category}, Limit: {budget.limit:.2f}, Spent: {budget.spent:.2f}")
            except EOFError:
                break

def main():
    # Authentication
    username = input("Enter username: ")
    password = input("Enter password: ")
    
    if not authenticate(username, password):
        print("Invalid credentials.")
        return

    print("Login successful!")
    
    while True:
        print("\n1. Add Expense")
        print("2. List Expenses")
        print("3. Set Budget")
        print("4. Update Budget")
        print("5. List Budgets")
        print("6. Exit")
        
        choice = input("Enter choice: ")

        if choice == '1':
            add_expense()
        elif choice == '2':
            list_expenses()
        elif choice == '3':
            set_budget()
        elif choice == '4':
            category = input("Enter budget category: ")
            amount = float(input("Enter amount to add to the budget: "))
            update_budget(category, amount)
        elif choice == '5':
            list_budgets()
        elif choice == '6':
            break
        else:
            print("Invalid choice.")

if __name__ == "__main__":
    main()
