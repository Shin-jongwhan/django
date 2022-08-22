# django web tutorial !
## 220807
## 인스타그램 클론 만들기
### 강의
#### https://www.youtube.com/watch?v=M8UPyeF5DfM&t=3895s
### 참고 사이트
- google material icon <br/> https://fonts.google.com/?selected=Material+Icons&icon.style=Rounded
- google material policy and css link 등 <br/> https://developers.google.com/fonts/docs/material_icons#icon_font_for_the_web
- bootstrap <br/> https://getbootstrap.kr/ 
### <br/>

### 링크
```
<!-- Bootstrap CSS -->
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-1BmE4kWBq78iYhFldvKuhfTAU6auU8tT94WrHftjDbrCEXSU1oBoqyl2QvZ6jIW3" crossorigin="anonymous">

<!-- google materials icon -->
<link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">
<link href="https://fonts.googleapis.com/css?family=Material+Icons|Material+Icons+Outlined|Material+Icons+Two+Tone|Material+Icons+Round|Material+Icons+Sharp" rel="stylesheet">

<!-- Jquery -->
<script  src="http://code.jquery.com/jquery-latest.min.js"></script>
```

## <br/><br/><br/>

## djnago 실행
### django 프로젝트 생성하기(자신의 프로젝트 경로로 가서 실행한다)
```
django-admin startproject mysite
```
#### <br/>

### 웹서버 실행
```
python manage.py runserver
```
### <br/><br/><br/>

## 웹페이지 기본 틀 만들기
### 기본 틀 잡기
![image](https://user-images.githubusercontent.com/62974484/183278548-dd2542f9-3616-409f-94ff-1df871c9776a.png) <br/>
### <br/><br/><br/>

### 왼쪽 피드 틀
![image](https://user-images.githubusercontent.com/62974484/183297736-94472703-bcf1-4460-b6a9-e42f6d1a8c2d.png) <br/>
### <br/><br/><br/>

### 오른쪽 추천인 틀
![image](https://user-images.githubusercontent.com/62974484/183300174-6ff04a6f-b263-4e2a-bfa8-554b401e1a4a.png) <br/>
### <br/><br/><br/> 

### 더미 완성본
https://user-images.githubusercontent.com/62974484/185751152-9c4a71f4-8163-4956-a733-beaca595a685.mp4

## <br/><br/><br/> 


## DB 생성하기
### django 에서는 models 라는 것을 불러와서 쓴다. 그리고 만든 models.py 를 실행하면 0001_initial.py 같은 스크립트가 하나 생성된다. 이게 DB 를 담고 있는 스크립트이다.
#### 이후 다음의 명령어를 실행하면 models.py 에 있는 객체가 DB 로 생기게 된다.
```
python manage.py makemigrations instagram_clone
```
##### models.py 위치
![image](https://user-images.githubusercontent.com/62974484/185752864-e799bcd8-cba8-4df5-bbcc-ec726ea7c978.png) 
##### 실행 후
![image](https://user-images.githubusercontent.com/62974484/185752994-48ccef51-8b5d-4623-9d91-faac12b28a4b.png)
#### django 는 기본적으로 db.sqlite3 라는 db 파일이 생성된다.
![image](https://user-images.githubusercontent.com/62974484/185753348-75e96d90-581a-4ac3-9bfa-13853057ed01.png)
#### migrate 를 하면 여러가지 기본 모델을 불러오고 내가 만든 모델 또한 불러온다.
```
python manage.py migrate
```
![image](https://user-images.githubusercontent.com/62974484/185753444-e02967f8-11a7-4b87-b059-d39ae91fa614.png)

### <br/><br/><br/>

### sqlite DB
#### 만약 불러온 db 를 보고싶다면, vscode 를 쓴다면 sqlite 를 설치하고 command pallete (ctrl + shift + P) 에서 SQLite: Open db 를 이용한다.
#### 그러면 왼쪽 하단에 EXPLORE DB 창이 생기고 DB 를 확인할 수 있다.
![image](https://user-images.githubusercontent.com/62974484/185755939-f5055654-796b-473b-b5e8-b51eb12767fd.png)
#### 특정 테이블에 우클릭하면 쿼리를 생성할 수 있고 테이블과 컬럼 정보 등을 조회할 수 있다.
#### 쿼리 실행은 ctrl + shift + Q
![image](https://user-images.githubusercontent.com/62974484/185755977-f312f3d2-74a9-42e7-994d-c6b557502bad.png)

### <br/>

### 테이블에 정보 추가하기
```
INSERT INTO instagram_clone_feed (content, image, profile_image, user_id, like_count) 
    VALUES ("우마무스메 컨디션 상승 이벤트", "https://static.inven.co.kr/column/2022/06/28/news/i15295595820.png", "https://user-images.githubusercontent.com/62974484/183277851-02f0c8af-35d4-4bec-9c03-9a2b3bf3391e.PNG", "우마무스메_OFFICIAL", 12345);
```
### 테이블에 정보 삭제하기
```
-- DELETE FROM 테이블명 where 조건식;
DELETE FROM instagram_clone_feed 
    WHERE id = 2;
```
![image](https://user-images.githubusercontent.com/62974484/185756787-d3cb1e7e-5c8a-49b9-85ec-af0576fc5a8d.png)
### <br/> 

### views.py
#### from .models import Feed 는 db.sqlite3 에 들어갔고, 그 안에 정보들을 생성해주었다. 
#### 그래서 models.py 에 있는 것이 DB 가 되고 djnago 는 이를 이용해 정보를 조회할 수 있다.
![image](https://user-images.githubusercontent.com/62974484/185757724-365e38ef-fe61-468a-9207-bfa221cfffe5.png)

### url.py
#### 불러올 url 스크립트를 import 하고 지정한다.
![image](https://user-images.githubusercontent.com/62974484/185757600-88d38331-2122-4690-b7d5-ad216863466e.png)

#### 웹페이지를 새로고침하면 출력된 것을 확인할 수 있다.
![image](https://user-images.githubusercontent.com/62974484/185757989-6552f9d9-cd0a-4be4-acc0-aa46d5c71fd4.png)

## <br/><br/><br/>

## 중간 점검
### DB 테이블을 다음과 같이 만들었다.
![image](https://user-images.githubusercontent.com/62974484/185759060-0687149a-5221-427e-bfd9-7146acc43550.png)

### 컨텐츠 조회는 html 상에서 DB 테이블에 row 수 만큼 for 문으로 이루어진다.
https://user-images.githubusercontent.com/62974484/185759170-996c3165-85e0-4927-8d12-17cfcfea8ef2.mp4


## <br/><br/><br/> 

## 이미지 파일 업로드 화면 만들기(모달)
### Jquery, javascript 를 사용한다.
#### 사진 업로드 구현
https://user-images.githubusercontent.com/62974484/185799246-9dfe6c35-65f7-42f7-a140-8a13e0c70631.mp4

## <br/><br/><br/>

## 서버로 파일 업로드하는 API 만들기
### API 는 ajax 를 이용하여 만든다.
### AJAX : Asynchronous JavaScript and XML
#### 비동기적으로 자바스크립트를 이용하여 정보를 교환하는 방식이다.
#### 서버에 요청을 하면 서버에는 요청을 받고, 웹페이지에서는 그 요청이 끝날 때까지 기다리지 않고 사용할 수 있도록 한다.
### 업로드 버튼을 누르면 피드가 업데이트된다.
https://user-images.githubusercontent.com/62974484/185976857-68c0a507-f86c-400e-8f9f-fde87622f7d9.mp4
### DB 도 같이 업데이트되고 왼쪽에 media 폴더에 보면 이미지 파일도 업로드가 된다.
https://user-images.githubusercontent.com/62974484/185976501-f38ad4ab-7839-4466-8a61-2818e2c971ce.mp4


