"use client";

import { useState } from "react";

export default function Home() {
  const [tasks, setTasks] = useState([]);
  const [input, setInput] = useState("");

  // 할 일 추가
  const addTask = () => {
    if (input.trim() === "") return;

    if (tasks.length >= 10) {
      alert("할 일은 최대 10개까지 가능합니다!");
      return;
    }

    const newTask = {
      text: input,
      done: false,
    };

    setTasks([...tasks, newTask]);
    setInput("");
  };

  // 체크 기능
  const toggleTask = (index) => {
    const newTasks = [...tasks];
    newTasks[index].done = !newTasks[index].done;
    setTasks(newTasks);
  };

  // 점수 계산
  const score = tasks.filter((task) => task.done).length;

  return (
    <main className="min-h-screen bg-gray-100 p-8">
      <div className="max-w-xl mx-auto bg-white rounded-2xl shadow-lg p-6">

        <h1 className="text-3xl font-bold text-center mb-6">
          오늘의 점수
        </h1>

        {/* 점수 */}
        <div className="mb-6">
          <div className="text-center text-5xl font-bold">
            {score} / 10
          </div>

          <div className="w-full bg-gray-200 rounded-full h-6 mt-4">
            <div
              className="bg-green-500 h-6 rounded-full transition-all"
              style={{ width: `${score * 10}%` }}
            ></div>
          </div>
        </div>

        {/* 입력창 */}
        <div className="flex gap-2 mb-6">
          <input
            type="text"
            value={input}
            onChange={(e) => setInput(e.target.value)}
            placeholder="오늘 할 일을 입력하세요"
            className="flex-1 border rounded-xl p-3 outline-none"
          />

          <button
            onClick={addTask}
            className="bg-black text-white px-5 rounded-xl"
          >
            추가
          </button>
        </div>

        {/* 할 일 목록 */}
        <div className="space-y-3">
          {tasks.map((task, index) => (
            <div
              key={index}
              className="flex items-center gap-3 bg-gray-50 p-3 rounded-xl"
            >
              <input
                type="checkbox"
                checked={task.done}
                onChange={() => toggleTask(index)}
                className="w-5 h-5"
              />

              <span
                className={
                  task.done
                    ? "line-through text-gray-400"
                    : ""
                }
              >
                {task.text}
              </span>
            </div>
          ))}
        </div>

      </div>
    </main>
  );
}
