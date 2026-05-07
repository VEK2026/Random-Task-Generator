import tkinter as tk
from tkinter import messagebox, ttk
import random
import json
import os

# Путь к файлу истории
HISTORY_FILE = "tasks.Json"

class RandomTaskGenerator:
 def __init__(self, root):
 self.Root = root
 self.Root.Title("Random Task Generator")
 self.Root.Geometry("600x500")

 # Список предопределённых задач
 self.Tasks = [
 {"type": "учёба", "task": "Прочитать статью"},
 {"type": "спорт", "task": "Сделать зарядку"},
 {"type": "работа", "task": "Ответить на письма"},
 {"type": "быт", "task": "Помыть посуду"},
 {"type": "творчество", "task": "Нарисовать эскиз"}
]

 self.Load_history()

 self.Setup_ui()

 def setup_ui(self):
 # Заголовок
 tk.Label(self.Root, text="Генератор случайных задач", font=("Arial", 16)).Pack(pady=10)

 # Кнопка генерации
 tk.Button(self.Root, text="Сгенерировать задачу", command=self.Generate_task).Pack(pady=5)

 # Поле для ввода новой задачи
 tk.Label(self.Root, text="Добавить новую задачу:").Pack()
 self.New_task_input = tk.Entry(self.Root, width=50)
 self.New_task_input.Pack(pady=5)

 tk.Button(self.Root, text="Добавить задачу", command=self.Add_task).Pack(pady=5)

 # Фильтрация
 tk.Label(self.Root, text="Фильтр по типу:").Pack()
 self.Filter_var = tk.StringVar(value="все")
 filters = ["все", "учёба", "спорт", "работа", "быт", "творчество"]
 for filter in filters:
 tk.Radiobutton(self.Root, text=filter, variable=self.Filter_var, value=filter).Pack(anchor="w", padx=20)

 # Список задач
 self.Task_list = tk.Listbox(self.Root, width=60, height=15)
 self.Task_list.Pack(pady=10)

 # Обновление списка
 self.Update_task_list()

 def generate_task(self):
 task = random.Choice(self.Tasks)
 self.History.Append(task)
 self.Save_history()
 self.Update_task_list()
 messagebox.Showinfo("Задача", f"Ваша задача: {task['task']} (тип: {task['type']})")

 def add_task(self):
 new_task = self.New_task_input.Get().Strip()
 if not new_task:
 messagebox.Showerror("Ошибка", "Задача не может быть пустой!")
 return

 # Спрашиваем тип задачи
 task_type = messagebox.Askstring("Тип задачи", "Введите тип задачи (учёба, спорт, работа, быт, творчество):", initialvalue="учёба")
 if task_type not in ["учёба", "спорт", "работа", "быт", "творчество"]:
 messagebox.Showerror("Ошибка", "Неверный тип задачи!")
 return

 self.Tasks.Append({"type": task_type, "task": new_task})
 self.New_task_input.Delete(0, tk.END)
 messagebox.Showinfo("Успех", "Задача добавлена!")

 def load_history(self):
 if os.Path.Exists
