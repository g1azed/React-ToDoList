# React-ToDoList
> 리액트로 간단한 투두리스트 구현해보기

[![NPM Version][npm-image]][npm-url]
[![Build Status][travis-image]][travis-url]
[![Downloads Stats][npm-downloads]][npm-url]

한 두 문단으로 프로젝트 소개 글을 작성합니다.

![](../header.png)

## 구현 기능 리스트

* 글자 제출
    ```
        const handleAddTodo = () => {
        if (inputValue.trim() !== '') {
            const isDuplicate = todos.some((todo) => todo.text === inputValue);
            if (isDuplicate) {
                alert('이미 추가된 할 일입니다.');
            } else if (inputValue.length > 20) {
                alert('할 일은 20자 이하로 입력해주세요.');
            } else {
                setTodos([...todos, { text: inputValue, checked: false }]);
            }
            setInputValue('');
        }
    };
    ```
    * 이미 제출 된 리스트 중 제출하려는 리스트와 중복될 시 제출 금지
    * 글자 수가 20자 이상일 때에는 제출 금지
    * *some() : 배열 안의 어떤 요소라도 주어진 판별 함수를 적어도 하나라도 통과하는지 테스트하는 JS메서드
    * *trim() : 양 끝의 공백을 제거하고 원본 문자열 그대로 다시 새로운 문자열로 반환하는 JS메서드
* 글자 삭제
```
    const handleDeleteTodo = (index) => {
        const updatedTodos = todos.filter((_, i) => i !== index);
        setTodos(updatedTodos);
    };
```
    * 수정: `setDefaultXYZ()` 메서드 제거
    * 추가: `init()` 메서드 추가
* 해낸 일 체크
    * 버그 수정: `baz()` 메서드 호출 시 부팅되지 않는 현상 (@컨트리뷰터 감사합니다!)
* 전체 삭제
    * 첫 출시
    * 수정: `foo()` 메서드 네이밍을 `bar()`로 수정


## 전체코드
```
import React, { useState } from 'react';
import './reset.css'
import './todolist.css'

function TodoList() {
    const [todos, setTodos] = useState([]);
    const [inputValue, setInputValue] = useState('');

    const handleInputChange = (e) => {
        setInputValue(e.target.value);
    };

    const handleAddTodo = () => {
        if (inputValue.trim() !== '') {
            const isDuplicate = todos.some((todo) => todo.text === inputValue);
            if (isDuplicate) {
                alert('이미 추가된 할 일입니다.');
            } else if (inputValue.length > 20) {
                alert('할 일은 20자 이하로 입력해주세요.');
            } else {
                setTodos([...todos, { text: inputValue, checked: false }]);
            }
            setInputValue('');
        }
    };


    const handleToggleTodo = (index) => {
        const updatedTodos = todos.map((todo, i) => {
            if (i === index) {
                return { ...todo, checked: !todo.checked };
            }
            return todo;
        });
        setTodos(updatedTodos);
    };

    const handleDeleteTodo = (index) => {
        const updatedTodos = todos.filter((_, i) => i !== index);
        setTodos(updatedTodos);
    };

    const handleDeleteAll = () => {
        setTodos([]);
    };

    return (
        <div>
            <h1> THINGS TO DO : </h1>
            <div className="add-wrap">
                <input
                    type="text"
                    value={inputValue}
                    onChange={handleInputChange}
                    placeholder="Enter a todo"
                />
                <button className="btn add-btn" onClick={handleAddTodo}> Add </button>
                <button className="btn delete-all-btn" onClick={handleDeleteAll}>Delete All</button>
            </div>

            <ul>
                {todos.map((todo, index) => (
                    <li
                        key={index}
                        style={{ textDecoration: todo.checked ? 'line-through' : 'none' }}
                        className="list-li"
                    >
                        <input
                            type="checkbox"
                            checked={todo.checked}
                            onChange={() => handleToggleTodo(index)}
                        />
                        <p className="list-text"> {todo.text} </p>
                        <button className="btn delete-btn"onClick={() => handleDeleteTodo(index)}>Delete</button>
                    </li>
                ))}
            </ul>
        </div>
    );
}

export default TodoList;
```

