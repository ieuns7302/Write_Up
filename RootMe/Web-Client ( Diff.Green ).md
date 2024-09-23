# 🟢 RootMe Difficult Green All Write Up( Web-Client )

https://www.root-me.org/en/Challenges/Web-Client/

## 목차

1. [🧑🏻‍💻 HTML > disabled buttons](#🧑🏻‍💻-html->-disabled-buttons)
2. [🧑🏻‍💻 Javascript > Authentication](#🧑🏻‍💻-javascript->-authentication)
3. [🧑🏻‍💻 Javascript > Source](#🧑🏻‍💻-javascript->-source)
4. [🧑🏻‍💻 Javascript > Authentication 2](#🧑🏻‍💻-javascript->-authentication-2)
5. [🧑🏻‍💻 Javascript > Obfuscation 1](#🧑🏻‍💻-javascript>-obfuscation-1)
6. [🧑🏻‍💻 Javascript > Obfuscation 2](#🧑🏻‍💻-javascript->-obfuscation-2)
---
</br>

## 🧑🏻‍💻 HTML > disabled buttons
> 해당 문제는 비활성화되어 있는 input과 button을 활성화시키는 문제이다.
</br>
문제를 살펴보니 각각 `disabled` 속성이 적용되어 있었다.

```Plain Text
[ disabled 속성 ]

- disabled 속성은 비활성화됨을 의미한다.
- disabled 속성이 명시된 태그는 사용할 수 없으며, 사용자가 클릭도 할 수 없다.
- 따라서 이 속성을 사용하면 특정 조건이 충족될 때까지 사용자가 버튼을 클릭할 수 없도록 설정하고,
  특정 조건이 충족되면 자바스크립트 등으로 disabled 속성 값을 삭제하여 다시 버튼을 사용할 수 있도록 조절할 수 있다.
- disabled 속성은 Boolean이다.
```

`disabled` 속성때문에 input과 button이 비활성화되어 있음으로 개발자모드를 통해 각각 태그들의 `disabled` 속성을 삭제하면 다시 활성화가 된다. </br></br>
활성화된 input에 아무런 값을 입력하고 button을 클릭하면 문제가 풀린다.
</br></br>

## 🧑🏻‍💻 Javascript > Authentication
> 해당 문제는 pw를 찾아 제출하면 풀리는 문제이다.
</br>
문제를 살펴보니 Username과 Password를 입력할 수 있는 로그인 기능이 구현되어 있는 페이지이다.

```javascript
function Login(){
    var pseudo=document.login.pseudo.value;
    var username=pseudo.toLowerCase();
    var password=document.login.password.value;
    password=password.toLowerCase();
    if (pseudo=="4dm1n" && password=="sh.org") {
        alert("Password accepté, vous pouvez valider le challenge avec ce mot de passe.\nYou an validate the challenge using this password.");
    }
    else {
        alert("Mauvais mot de passe / wrong password");
    }
}
```
</br>

개발자도구에 Source 탭에 가서 코드를 보니 위와 같이 `if`문을 사용해 로그인기능이 구현되있다.</br></br>
코드에서 `alert()` 안에 있는 <strong>You an validate the challenge using this password.</strong> 문구처럼, password 값인 `sh.org`를 입력하니 문제가 풀렸다. 

</br></br>

## 🧑🏻‍💻 Javascript > Source
> 해당 문제는 처음에 뜨는 prompt에 알맞은 값을 입력하면 풀리는 문제이다.

문제에 들어가면 처음부터 `prompt`가 뜨고 다른 기능은 보이지 않는다. </br>
개발자모드로 코드를 살펴보면
</br>

```javascript
function login() {
    pass=prompt("Entrez le mot de passe / Enter password");
    if ( pass == "123456azerty" ) {
      alert("Mot de passe accepté, vous pouvez valider le challenge avec ce mot de passe.\nYou can validate the challenge using this password.");
    }
    else {
      alert("Mauvais mot de passe / wrong password !");
    }
}
```
</br>

위의 코드와 같이 `pass = "123456azerty` 이면 문제가 풀리기에 처음 prompt 창에 "123456azerty"를 입력하면 문제가 풀린다.

</br></br>

## 🧑🏻‍💻 Javascript > Authentication 2
> 해당 문제는 올바른 username과 password를 입력하는 문제이다.
</br>

문제에 들어가니 `login`버튼이 존재했고 버튼을 누르니 `username`과 `password`를 입력하는 칸이 나온다.

```javascript
function connexion(){
    var username = prompt("Username :", "");
    var password = prompt("Password :", "");
    var TheLists = ["GOD:HIDDEN"];
    for (i = 0; i < TheLists.length; i++)
    {
        if (TheLists[i].indexOf(username) == 0)
        {
            var TheSplit = TheLists[i].split(":");
            var TheUsername = TheSplit[0];
            var ThePassword = TheSplit[1];
            if (username == TheUsername && password == ThePassword)
            {
                alert("Vous pouvez utiliser ce mot de passe pour valider ce challenge (en majuscules) / You can use this password to validate this challenge (uppercase)");
            }
        }
        else
        {
            alert("Nope, you're a naughty hacker.")
        }
    }
}
```
</br>

해당 코드를 보니 `:`를 기준으로 왼쪽 부분을 `TheUsername`에 할당해주고, 오른쪽 부분을 `ThePassword`를 할당해준다. </br></br>
따라서 `TheUsername`에는 `GOD`이 담기고, `ThePassword`에는 `HIDDEN`이 담긴다. </br></br>
username에는 `GOD`을 password에는 `HIDDEN`을 입력하니 문제가 풀렸다.

</br></br>

## 🧑🏻‍💻 Javascript > Obfuscation 1
> 해당 문제는 url encoding 된 값을 입력하면 풀리는 문제이다.
</br>

첫 화면에는 `prompt`를 통해 값을 받는 화면만 나오고 다른 기능은 보이지 않는다.

</br>

```javascript
pass = '%63%70%61%73%62%69%65%6e%64%75%72%70%61%73%73%77%6f%72%64';

h = window.prompt('Entrez le mot de passe / Enter password');
if(h == unescape(pass)) {
    alert('Password accepté, vous pouvez valider le challenge avec ce mot de passe.\nYou an validate the challenge using this pass.');
}
else {
    alert('Mauvais mot de passe / wrong password');
}
```
위의 코드에서 보이는 것 처럼 pass 안에는 `url encoding`된 값이 있고, 그 값을 통해 조건문을 만족해야하는 것 처럼 보인다. </br></br>
pass 안에 있는 값을 `url decoding` 해주면 `cpasbiendurpassword`라는 값이 나오고 입력하면 문제가 풀린다.

</br></br>

## 🧑🏻‍💻 Javascript > Obfuscation 2
> 해당 문제는 url decoding 후 ascii 변환을 한 값을 입력하면 풀리는 문제이다.

</br>
문제에 들어가니 빈 화면밖에 보이지 않는다. </br>

코드를 살펴보니
```javascript
var pass = unescape("unescape%28%22String.fromCharCode%2528104%252C68%252C117%252C102%252C106%252C100%252C107%252C105%252C49%252C53%252C54%2529%22%29");
```

</br>

위와 같이 pass라는 변수에 `url encoding`된 값이 담겨있다. </br>
불필요한 부분 날리고 decoding 하니 `(104,68,117,102,106,100,107,105,49,53,54)` 라는 값이 나와서 `ascii code`를 보고 바꿔보니 </br>
<strong>hDufjdki156</strong>라는 값이 나온다. 이 값을 입력하니 문제가 풀렸다.

---
</br>

<strong>잘못된 정보나 궁금한 점이 있으신 분은 Discord `ieuns`로 연락주시면 감사하겠습니다. ☺️</strong>
