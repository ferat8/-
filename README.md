# -main.py
from fastapi import FastAPI
from pydantic import BaseModel
from typing import List

app = FastAPI(title="ToDo App")

class Task(BaseModel):
    id: int
    title: str
    completed: bool = False

tasks: List[Task] = []

@app.get("/tasks")
def get_tasks():
    return tasks

@app.post("/tasks")
def create_task(task: Task):
    tasks.append(task)
    return task

@app.put("/tasks/{task_id}")
def update_task(task_id: int, updated_task: Task):
    for i, task in enumerate(tasks):
        if task.id == task_id:
            tasks[i] = updated_task
            return updated_task
    return {"error": "Task not found"}

@app.delete("/tasks/{task_id}")
def delete_task(task_id: int):
    for i, task in enumerate(tasks):
        if task.id == task_id:
            removed_task = tasks.pop(i)
            return removed_task
    return {"error": "Task not found"}

requirements.txt
fastapi
uvicorn

README.md
# 📝 ToDo App

Simple ToDo App using FastAPI.

## 🛠️ Tech Stack
- Python 3
- FastAPI
- Uvicorn

## 🚀 Run Locally
```bash
pip install -r requirements.txt
uvicorn main:app --reload

📚 Конец

GET /tasks- получить все задачи

POST /tasks- создать задачу

PUT /tasks/{task_id}- обновить задачу_

DELETE /tasks/{task_id}- принадлежащий_
