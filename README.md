import tkinter as tk
from tkinter import messagebox

# Function to add task
def add_task():
    task = entry_task.get()
    if task != "":
        listbox_tasks.insert(tk.END, task)
        entry_task.delete(0, tk.END)
    else:
        messagebox.showwarning("Warning", "Please enter a task!")

# Function to delete selected task
def delete_task():
    try:
        selected = listbox_tasks.curselection()[0]
        listbox_tasks.delete(selected)
    except:
        messagebox.showwarning("Warning", "Please select a task to delete!")

# Function to mark task as done
def mark_done():
    try:
        selected = listbox_tasks.curselection()[0]
        task = listbox_tasks.get(selected)
        listbox_tasks.delete(selected)
        listbox_tasks.insert(tk.END, f"✔ {task}")
    except:
        messagebox.showwarning("Warning", "Please select a task to mark done!")

# Main window
root = tk.Tk()
root.title("To-Do List")
root.geometry("300x400")

# Widgets
frame = tk.Frame(root)
frame.pack(pady=10)

listbox_tasks = tk.Listbox(frame, width=40, height=15, selectmode=tk.SINGLE)
listbox_tasks.pack(side=tk.LEFT, fill=tk.BOTH)

scrollbar = tk.Scrollbar(frame)
scrollbar.pack(side=tk.RIGHT, fill=tk.BOTH)

listbox_tasks.config(yscrollcommand=scrollbar.set)
scrollbar.config(command=listbox_tasks.yview)

entry_task = tk.Entry(root, width=35)
entry_task.pack(pady=5)

button_add = tk.Button(root, text="Add Task", width=12, command=add_task)
button_add.pack(pady=2)

button_delete = tk.Button(root, text="Delete Task", width=12, command=delete_task)
button_delete.pack(pady=2)

button_done = tk.Button(root, text="Mark Done", width=12, command=mark_done)
button_done.pack(pady=2)

root.mainloop()
