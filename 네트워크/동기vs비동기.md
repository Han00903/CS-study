## 🎯 동기(Synchronous) vs 비동기(Asynchronous) 처리
![image](https://github.com/user-attachments/assets/a0465ed8-cc44-4698-8b5f-56fe8c6fa819)
- 동기(Sync)와 비동기(Async)는 데이터나 작업이 처리되는 방식에 따라 구분할 수 있다.
- 즉, 웹에서 동기(Sync)와 비동기(Async) 방식은 요청과 응답이 처리되는 방식에 따라 구분한다. 
### 📌 동기(Synchronous)
- 동기 방식은 요청을 보낸 후 결과를 받을 때까지 기다리는 방식으로 하나의 작업이 완료되어야 다음 작업을 시작할 수 있다.
- 클라이언트나 서버는 요청을 처리하는 동안 다른 작업을 하지 못하고 결과가 오기를 기다려야 한다. 
- 웹에서 동기 방식은 요청을 보낸 후 응답을 받을 때까지 기다려야 하므로 **전체 페이지를 새로고침**해야한다.<br>
![image](https://github.com/user-attachments/assets/0d0fe5e3-4626-4aa9-b15c-247d4e5127d8)

```
💡동기 방식의 예

public String signUp(User user) {
    // 1. 데이터베이스에 회원가입 정보 저장
    database.save(user);
    
    // 2. 저장 완료 후 메시지 반환
    return "회원가입 성공";
}

✅ 동작 설명
- 클라이언트가 서버에 회원가입 요청을 보내면 서버는 DB에 정보를 저장한 후 저장이 완료될 때까지 기다린다.
- 저장이 완료된 후 "회원가입 성공"메시지를 클라이언트에 반환한다.
- 클라이언트는 다른 작업을 하지 못하고 응답을 기다려야 한다. 
```
✅ 장/단점<br>
-
  1️⃣ 장점<br>
  - 코드가 간결하고 직관적이다.
  - 요청과 응답의 순서를 보장할 수 있어 예측 가능한 흐름을 유지할 수 있다.
  - 에러 처리도 비교적 쉽다.
  2️⃣ 단점<br>
  - 요청을 보내고 응답을 받을 때까지 기다리므로 대기 시간이 길어질 수 있다.
  - 웹 페이지가 새로고침되거나 전체가 갱신되는 방식이 많아 성능 저하와 사용자 불편을 초래할 수 있다.
  - 동시에 여러 작업을 처리하기 어려운 단점이 존재한다.
### 📌 비동기(Asynchronous)
- 비동기 방식은 요청을 보낸 후 응답을 기다리지 않고 다른 작업을 즉시 처리할 수 있는 방식으로 서버는 요청을 받은 후 결과를 처리하면서도 클라이언트는 다른 작업을 할 수 있다.
- 비동기 방식은 웹 페이지 일부만을 동적으로 갱신할 수 있고 응답이 준비되면 콜백을 통해 결과를 처리한다.
![image](https://github.com/user-attachments/assets/d7c5e385-742e-4b89-9cdb-005c8e189c4a)
- 웹의 비동기 통신의 가장 대표적인 처리 기술은 AJAX(Asynchronous JavaScript And XML)이다.
![image](https://github.com/user-attachments/assets/4ed1db35-1d3a-47fd-9861-c85bbe1e69c3)

```
💡비동기 방식의 예
fetch('http://localhost:8080/api/users/signup', {
    method: 'POST',
    headers: {
        'Content-Type': 'application/json',
    },
    body: JSON.stringify(userData)  // JSON 형식으로 데이터를 전송
})
.then(response => response.json())
.then(data => {
    // 서버에서 응답 받은 후 처리하는 부분
    if (data.message) {
        alert('회원가입 성공: ' + data.message);
        window.location.href = "/signin";  // 로그인 페이지로 리다이렉트
    }
})
.catch(error => {
    console.error('Error:', error);
    document.getElementById("error-message").style.display = 'block';  // 실패 메시지 표시
});

✅ 동작 설명
- 클라이언트는 비동기적으로 요청을 보낸 후 응답을 기다리지 않고 바로 다른 작업을 할 수 있다.
- 서버는 요청을 받은 후 데이터를 처리하고 응답이 완료되면 클라이언트에 결과를 전달한다.
- 클라이언트는 .then()메서드를 통해 응답을 처리한다.
```
✅ 장/단점<br>
- 
  1️⃣ 장점<br>
  - 서버와의 통신 후 응답을 기다리지 않고 다른 작업을 수행할 수 있어 성능 향상과 사용자 경험 개선에 유리하다.
  - 대규모 요청 처리나 네트워크 요청과 같은 작업에서 뛰어난 성능을 발휘한다.
  - 화면이 멈추지 않고 부드럽게 작동하여 사용자 경험을 개선할 수 있다.
  2️⃣ 단점<br>
  - 코드가 복잡하고 이해하기 어려울 수 있다.
  - 요청의 처리 순서가 보장되지 않으므로 요청의 결과가 뒤죽박죽으로 처리될 수 있다.
  - 에러 처리가 복잡할 수 있다. 





참고문헌:
https://inpa.tistory.com/entry/WEB-%F0%9F%8C%90-%EB%B9%84%EB%8F%99%EA%B8%B0Async%ED%86%B5%EC%8B%A0-%EB%8F%99%EA%B8%B0Sync%ED%86%B5%EC%8B%A0
