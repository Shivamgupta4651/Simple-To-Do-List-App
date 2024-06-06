# Simple-To-Do-List-App
pip install tk
import tkinter as tk
from tkinter import messagebox
class ToDoApp:
    def __init__(self, root):
        self.root = root
        self.root.title("To-Do List Application")

        self.tasks = []

        self.frame = tk.Frame(root)
        self.frame.pack(pady=10)

        self.task_listbox = tk.Listbox(
            self.frame, 
            height=10, 
            width=50, 
            selectmode=tk.SINGLE
        )
        self.task_listbox.pack(side=tk.LEFT, fill=tk.BOTH)

        self.scrollbar = tk.Scrollbar(self.frame)
        self.scrollbar.pack(side=tk.RIGHT, fill=tk.BOTH)

        self.task_listbox.config(yscrollcommand=self.scrollbar.set)
        self.scrollbar.config(command=self.task_listbox.yview)

        self.task_entry = tk.Entry(root, width=50)
        self.task_entry.pack(pady=10)

        self.add_button = tk.Button(
            root, 
            text="Add Task", 
            width=48, 
            command=self.add_task
        )
        self.add_button.pack(pady=10)

        self.remove_button = tk.Button(
            root, 
            text="Remove Task", 
            width=48, 
            command=self.remove_task
        )
        self.remove_button.pack(pady=10)

        self.mark_button = tk.Button(
            root, 
            text="Mark as Completed", 
            width=48, 
            command=self.mark_completed
        )
        self.mark_button.pack(pady=10)

    def add_task(self):
        task = self.task_entry.get()
        if task != "":
            self.tasks.append(task)
            self.update_task_listbox()
            self.task_entry.delete(0, tk.END)
        else:
            messagebox.showwarning("Warning", "You must enter a task.")

    def remove_task(self):
        task_index = self.task_listbox.curselection()
        if task_index:
            task_index = task_index[0]
            del self.tasks[task_index]
            self.update_task_listbox()
        else:
            messagebox.showwarning("Warning", "You must select a task to remove.")

    def mark_completed(self):
        task_index = self.task_listbox.curselection()
        if task_index:
            task_index = task_index[0]
            task = self.tasks[task_index]
            self.tasks[task_index] = f"{task} (completed)"
            self.update_task_listbox()
        else:
            messagebox.showwarning("Warning", "You must select a task to mark as completed.")

    def update_task_listbox(self):
        self.task_listbox.delete(0, tk.END)
        for task in self.tasks:
            self.task_listbox.insert(tk.END, task)


if __name__ == "__main__":
    root = tk.Tk()
    app = ToDoApp(root)
    root.mainloop()

