# React-ToDoList
> 리액트로 간단한 투두리스트 구현해보기

# 🔗구현 링크
https://g1azed.github.io/React-ToDoList/
(무슨오류인지 빈페이지만 뜨네요 고쳐서 다음주부터는 잘 배포해보도록하겠습니다)

## 구현 기능 리스트

* useState 

```
    const [todos, setTodos] = useState([]);
    const [inputValue, setInputValue] = useState('');
```

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
    * 

* 해낸 일 체크
```
    const handleToggleTodo = (index) => {
        const updatedTodos = todos.map((todo, i) => {
            if (i === index) {
                return { ...todo, checked: !todo.checked };
            }
            return todo;
        });
        setTodos(updatedTodos);
    };
```


* 전체 삭제
```
    const handleDeleteAll = () => {
        setTodos([]);
    };
```


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

