# Human_resource_management

import tkinter as tk
from tkinter import messagebox

class EmployeeManagementSystem:
    def __init__(self, root):
        self.root = root
        self.root.title("Employee Management System")

        self.data = []
        self.create_header()
        self.create_table()
        self.create_calculate_button()

    def create_header(self):
        header_label = tk.Label(self.root, text="Monthly Attendance Sheet", font=("bold", 16), fg="red")
        header_label.grid(row=0, columnspan=3, pady=10)

    def create_table(self):
        columns = ["Sr No", "Date", "Attendance Record"]

        for col_idx, col_name in enumerate(columns):
            label = tk.Label(self.root, text=col_name, padx=10, pady=5, font=("bold"))
            label.grid(row=1, column=col_idx)
            label.config(bg="blue", fg="white")  # Add blue background and white text color to headers

        for row_idx in range(2, 17):
            sr_no = tk.Label(self.root, text=row_idx - 1, font=("bold"))
            sr_no.grid(row=row_idx, column=0)

            date_entry = tk.Entry(self.root)
            date_entry.grid(row=row_idx, column=1)

            attendance_entry = tk.Entry(self.root)
            attendance_entry.grid(row=row_idx, column=2)

            self.data.append({"date": date_entry, "attendance": attendance_entry})

    def calculate_salary(self):
        total_salary = 0
        for entry in self.data:
            attendance = entry["attendance"].get()
            if attendance == "A":
                total_salary += 0  # Adjust this as needed
            elif attendance == "P":
                total_salary += 1000  # Adjust this as needed
            else:
                messagebox.showerror("Error", f"Invalid attendance record for Sr No {self.data.index(entry) + 1}")

        messagebox.showinfo("Salary Calculation", f"Total Salary: {total_salary}")

    def create_calculate_button(self):
        calculate_button = tk.Button(self.root, text="Calculate Salary", command=self.calculate_salary, font=("bold"))
        calculate_button.grid(row=17, columnspan=3, pady=10)

if __name__ == "__main__":
    root = tk.Tk()
    app = EmployeeManagementSystem(root)
    root.mainloop()
