# Webhacking.kr > old-06

https://webhacking.kr/challenge/web-06/
* score : 10

## 문제 설명
* 첫 화면에는 오직 ID : guest, PW : 123qwe 라는 정보만 존재한다.

<strong>[ KEY CODE ]</strong>
```PHP
for($i=0;$i<20;$i++){
  $decode_id=base64_decode($decode_id);
  $decode_pw=base64_decode($decode_pw);
}
...
 
if($decode_id=="admin" && $decode_pw=="nimda"){
  solve(6);
}
```
위의 코드와 함께 문제를 풀기 위해 살펴보면..
* id, pw의 값을 총 20번 base64 디코딩한다.
* decode_id 값이 <strong>"admin"</strong>, decode_pw 값이 <strong>"nimda"</strong>이면 6번 문제가 풀리도록 되어 있다.

## 문제 해결
"admin" 과 "nimda" 라는 값을 20번 base64 인코딩하기 위해 python으로 코드를 작성하였다.
```python
import base64

id = "admin".encode()
pw = "nimda".encode()

for i in range(20):
  id = base64.b64encode(id)
  pw = base64.b64encode(pw)

print(f'id : {id}')
print(f'pw : {pw}')
```

위의 코드를 실행한 후 나온 id, pw 값을</br>
user에 id 값을 password에는 pw 값으로 바꿔주면 문제가 풀리게 된다.
