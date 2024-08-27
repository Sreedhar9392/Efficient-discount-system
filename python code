import tkinter as tk
from tkinter import messagebox
import pandas as pd
import numpy as np

def create_account():
    create_account_window = tk.Toplevel(root)
    create_account_window.title("Create Account")

    new_id_label = tk.Label(create_account_window, text="New Customer ID:", font=("Arial", 12), bg="yellow")
    new_id_label.pack()

    new_id_entry = tk.Entry(create_account_window, font=("Arial", 12))
    new_id_entry.pack()

    new_name_label = tk.Label(create_account_window, text="Customer Name:", font=("Arial", 12), bg="yellow")
    new_name_label.pack()

    new_name_entry = tk.Entry(create_account_window, font=("Arial", 12))
    new_name_entry.pack()

    def create():
        global nparr
        new_customer_id = int(new_id_entry.get())
        new_customer_name = new_name_entry.get()
        new_customer_data = [new_customer_id, new_customer_name, 0]

        # Append the new customer data to the existing data
        nparr = np.vstack([nparr, new_customer_data])
        DF = pd.DataFrame(nparr, columns=["Customer ID", "Customer Name", "Visits"])
        DF.to_excel("customer_data.xlsx", index=False)

        create_account_window.destroy()
        open_main_gui(new_customer_id)

    create_button = tk.Button(create_account_window, text="Create Account", command=create, bg="green", fg="white",
                              font=("Arial", 14, "bold"))
    create_button.pack()

def open_main_gui(customer_id):
    main_window = tk.Toplevel(root)
    main_window.title("Food Outlet")

    # Rest of the main GUI code
    # ...

    # Display the information in the new GUI
    update_data(customer_id)

def update_data(customer_id):
    global nparr
    original_price = float(price_entry.get())

    visits = 0
    discount = 0
    name = ""

    for x in nparr:
        if x[0] == customer_id:
            visits = x[2]
            name = x[1]
            x[2] = x[2] + 1
            break

    if visits <= 9:
        discount = 0
    elif 10 <= visits <= 19:
        discount = 2
    elif 20 <= visits <= 29:
        discount = 8
    else:
        discount = 15

    new_price = original_price - (original_price * (discount / 100))

    visit_count_label.config(text=f"Visits: {visits}", fg="green", font=("Helvetica", 14, "bold"), bg="yellow")
    name_label.config(text=f"Customer Name: {name}", fg="orange", font=("Helvetica", 14, "bold"), bg="yellow")
    new_price_label.config(
        text=f"New Price after {discount} percent discount: ₹{new_price:.2f}", fg="blue",
        font=("Helvetica", 14, "bold"), bg="yellow")

    # Update the DataFrame and save it to the Excel file
    DF = pd.DataFrame(nparr, columns=["Customer ID", "Customer Name", "Visits"])
    DF.to_excel("customer_data.xlsx", index=False)

    # Show a dialog box for "Changes Incorporated"
    messagebox.showinfo("Changes Incorporated", "Changes have been incorporated.")

# Read customer data from Excel
df = pd.read_excel("customer_data.xlsx")
nparr = df.to_numpy()

# GUI setup
root = tk.Tk()
root.title("Food Outlet")
root.configure(bg="yellow")  # Set background color
bg_image = tk.PhotoImage(file="background_image.png")  # Replace with your image file
bg_label = tk.Label(root, image=bg_image)
bg_label.place(relwidth=1, relheight=1)

visit = tk.Label(root, text="Efficient Discount System", fg="red", font=("Arial", 18, "bold"), bg="yellow")
visit.pack()

# Rest of the main GUI code
customer_id_label = tk.Label(root, text="Customer ID:", font=("Arial", 12), bg="yellow")
customer_id_label.pack()

customer_id_entry = tk.Entry(root, font=("Arial", 12))
customer_id_entry.pack()

price_label = tk.Label(root, text="Original Price (₹):", font=("Arial", 12), bg="yellow")
price_label.pack()

price_entry = tk.Entry(root, font=("Arial", 12))
price_entry.pack()

# Initiate the login process when the customer ID is entered
def check_customer_id():
    customer_id = int(customer_id_entry.get())
    if any(nparr[:, 0] == customer_id):
        open_main_gui(customer_id)
    else:
        messagebox.showinfo("Customer Not Found", "Customer ID not found. Please create a new account.")
        create_account()

check_button = tk.Button(root, text="Update visits/check ID", command=check_customer_id, bg="blue", fg="white",
                         font=("Arial", 14, "bold"))
check_button.pack()

# Rest of the main GUI code
visit_count_label = tk.Label(root, text="Visits: N/A", font=("Arial", 12), bg="yellow")
visit_count_label.pack()

name_label = tk.Label(root, text="Name: N/A", font=("Arial", 12), bg="yellow")
name_label.pack()

new_price_label = tk.Label(root, text="New Price: N/A", font=("Arial", 12), bg="yellow")
new_price_label.pack()

# Restart button to reset the GUI
def restart():
    global nparr
    nparr = df.to_numpy()
    customer_id_entry.delete(0, tk.END)
