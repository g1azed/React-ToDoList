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
* 글자 삭제
    * 수정: `setDefaultXYZ()` 메서드 제거
    * 추가: `init()` 메서드 추가
* 해낸 일 체크
    * 버그 수정: `baz()` 메서드 호출 시 부팅되지 않는 현상 (@컨트리뷰터 감사합니다!)
* 전체 삭제
    * 첫 출시
    * 수정: `foo()` 메서드 네이밍을 `bar()`로 수정


## 정보

이름 – [@트위터 주소](https://twitter.com/dbader_org) – 이메일주소@example.com

XYZ 라이센스를 준수하며 ``LICENSE``에서 자세한 정보를 확인할 수 있습니다.

[https://github.com/yourname/github-link](https://github.com/dbader/)

## 기여 방법

1. (<https://github.com/yourname/yourproject/fork>)을 포크합니다.
2. (`git checkout -b feature/fooBar`) 명령어로 새 브랜치를 만드세요.
3. (`git commit -am 'Add some fooBar'`) 명령어로 커밋하세요.
4. (`git push origin feature/fooBar`) 명령어로 브랜치에 푸시하세요. 
5. 풀리퀘스트를 보내주세요.

<!-- Markdown link & img dfn's -->
[npm-image]: https://img.shields.io/npm/v/datadog-metrics.svg?style=flat-square
[npm-url]: https://npmjs.org/package/datadog-metrics
[npm-downloads]: https://img.shields.io/npm/dm/datadog-metrics.svg?style=flat-square
[travis-image]: https://img.shields.io/travis/dbader/node-datadog-metrics/master.svg?style=flat-square
[travis-url]: https://travis-ci.org/dbader/node-datadog-metrics
[wiki]: https://github.com/yourname/yourproject/wiki
