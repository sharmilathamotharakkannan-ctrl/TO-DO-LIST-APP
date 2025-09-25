import React, { useState } from "react";

function TodoApp() {
  const [task, setTask] = useState("");
  const [tasks, setTasks] = useState([]);

  // Add a new task
  const addTask = () => {
    if (task.trim() !== "") {
      setTasks([...tasks, { id: Date.now(), title: task, completed: false }]);
      setTask("");
    }
  };

  // Toggle task completed state
  const toggleComplete = (id) => {
    setTasks(
      tasks.map((task) =>
        task.id === id ? { ...task, completed: !task.completed } : task
      )
    );
  };

  // Delete a task
  const deleteTask = (id) => {
    setTasks(tasks.filter((task) => task.id !== id));
  };

  // Handle Enter key press in input
  const handleKeyPress = (e) => {
    if (e.key === "Enter") addTask();
  };

  return (
    <div style={{ maxWidth: 400, margin: "auto", fontFamily: "Arial, sans-serif" }}>
      <h2>Simple To-Do List</h2>
      <input
        type="text"
        placeholder="Add new task"
        value={task}
        onChange={(e) => setTask(e.target.value)}
        onKeyPress={handleKeyPress}
        style={{ padding: 8, width: "70%", marginRight: 8 }}
      />
      <button onClick={addTask} style={{ padding: "8px 12px" }}>Add</button>

      <ul style={{ listStyle: "none", padding: 0, marginTop: 20 }}>
        {tasks.map((task) => (
          <li key={task.id} style={{ marginBottom: 10, display: "flex", alignItems: "center" }}>
            <input
              type="checkbox"
              checked={task.completed}
              onChange={() => toggleComplete(task.id)}
              style={{ marginRight: 8 }}
            />
            <span style={{ flexGrow: 1, textDecoration: task.completed ? "line-through" : "none" }}>
              {task.title}
            </span>
            <button onClick={() => deleteTask(task.id)} style={{ marginLeft: 8 }}>Delete</button>
          </li>
        ))}
      </ul>
    </div>
  );
}

export default TodoApp;
