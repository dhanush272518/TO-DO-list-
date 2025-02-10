# TO-DO-list-
using tkinter for create, update and tasking to-do list
import tkinter as tk
from tkinter import messagebox

class TodoApp:
    def __init__(self, root):
        self.root = root
        self.root.title("To-Do List App")

        # Create a listbox to display tasks
        self.task_listbox = tk.Listbox(self.root, height=10, width=50, selectmode=tk.SINGLE)
        self.task_listbox.pack(pady=20)

        # Create an entry box to add new tasks
        self.task_entry = tk.Entry(self.root, width=50)
        self.task_entry.pack(pady=10)

        # Create buttons to add, update, and delete tasks
        self.add_button = tk.Button(self.root, text="Add Task", command=self.add_task)
        self.add_button.pack(pady=5)

        self.update_button = tk.Button(self.root, text="Update Task", command=self.update_task)
        self.update_button.pack(pady=5)

        self.delete_button = tk.Button(self.root, text="Delete Task", command=self.delete_task)
        self.delete_button.pack(pady=5)

        self.tasks = []

    def add_task(self):
        task = self.task_entry.get()
        if task:
            self.tasks.append(task)
            self.update_task_listbox()
            self.task_entry.delete(0, tk.END)
        else:
            messagebox.showwarning("Warning", "Please enter a task.")

    def update_task_listbox(self):
        self.task_listbox.delete(0, tk.END)
        for task in self.tasks:
            self.task_listbox.insert(tk.END, task)

    def update_task(self):
        selected_task_index = self.task_listbox.curselection()
        if selected_task_index:
            new_task = self.task_entry.get()
            if new_task:
                self.tasks[selected_task_index[0]] = new_task
                self.update_task_listbox()
                self.task_entry.delete(0, tk.END)
            else:
                messagebox.showwarning("Warning", "Please enter a task.")
        else:
            messagebox.showwarning("Warning", "Please select a task to update.")

    def delete_task(self):
        selected_task_index = self.task_listbox.curselection()
        if selected_task_index:
            del self.tasks[selected_task_index[0]]
            self.update_task_listbox()
        else:
            messagebox.showwarning("Warning", "Please select a task to delete.")

if __name__ == "__main__":
    root = tk.Tk()
    app = TodoApp(root)
    root.mainloop()
