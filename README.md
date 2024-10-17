import tkinter as tk
from tkinter import messagebox
from PIL import Image, ImageTk  # Import Pillow for handling images

class ExpenseTracker:
    def __init__(self, root):
        self.root = root
        self.root.title("Expense Tracker")

        self.expenses = []

        # Load and display a logo at the top of the window
        self.logo_image = Image.open("C:\\Users\\ICT_user41\\Pictures\\Screenshots") 
        self.logo_image = self.logo_image.resize((100, 100), Image.ANTIALIAS)  # Resize logo
        self.logo_photo = ImageTk.PhotoImage(self.logo_image)
        self.label_logo = tk.Label(root, image=self.logo_photo)
        self.label_logo.grid(row=0, column=0, columnspan=2, padx=10, pady=10)

        # Labels and Entries for expense name and amount
        self.label_name = tk.Label(root, text="Expense Name:")
        self.label_name.grid(row=1, column=0, padx=10, pady=10)
        self.entry_name = tk.Entry(root)
        self.entry_name.grid(row=1, column=1, padx=10, pady=10)

        self.label_amount = tk.Label(root, text="Amount:")
        self.label_amount.grid(row=2, column=0, padx=10, pady=10)
        self.entry_amount = tk.Entry(root)
        self.entry_amount.grid(row=2, column=1, padx=10, pady=10)

        # Buttons
        self.button_add = tk.Button(root, text="Add Expense", command=self.add_expense)
        self.button_add.grid(row=3, column=0, columnspan=2, pady=10)

        self.button_show = tk.Button(root, text="Show Expenses", command=self.show_expenses)
        self.button_show.grid(row=4, column=0, columnspan=2, pady=10)

        # Listbox to show expenses
        self.listbox_expenses = tk.Listbox(root, width=50)
        self.listbox_expenses.grid(row=5, column=0, columnspan=2, padx=10, pady=10)

    def add_expense(self):
        name = self.entry_name.get()
        amount = self.entry_amount.get()

        if name and amount:
            try:
                amount = float(amount)
                self.expenses.append((name, amount))
                self.entry_name.delete(0, tk.END)
                self.entry_amount.delete(0, tk.END)
                messagebox.showinfo("Success", "Expense added successfully!")
            except ValueError:
                messagebox.showerror("Error", "Please enter a valid amount.")
        else:
            messagebox.showerror("Error", "Please fill in all fields.")

    def show_expenses(self):
        self.listbox_expenses.delete(0, tk.END)
        for name, amount in self.expenses:
            self.listbox_expenses.insert(tk.END, f"{name}: ${amount:.2f}")

if __name__ == "__main__":
    root = tk.Tk()
    app = ExpenseTracker(root)
    root.mainloop()
