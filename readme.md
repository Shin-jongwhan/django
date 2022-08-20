# django web tutorial !
## 220807
## 인스타그램 클론 만들기
### 강의
#### https://www.youtube.com/watch?v=M8UPyeF5DfM&t=3895s
### 참고 사이트
- google material icon <br/> https://fonts.google.com/?selected=Material+Icons&icon.style=Rounded
- google material policy and css link 등 <br/> https://developers.google.com/fonts/docs/material_icons#icon_font_for_the_web
- bootstrap <br/> https://getbootstrap.kr/ 

### <br/><br/><br/>

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
### <br/><br/><br/> 


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

#### 만약 불러온 db 를 보고싶다면, vscode 를 쓴다면 sqlite 를 설치하고 command pallete (ctrl + shift + P) 에서 SQLite: Open db 를 이용한다.
#### 그러면 왼쪽 하단에 EXPLORE DB 창이 생기고 DB 를 확인할 수 있다.
![image](https://user-images.githubusercontent.com/62974484/185755939-f5055654-796b-473b-b5e8-b51eb12767fd.png)
#### 특정 테이블에 우클릭하면 쿼리를 생성할 수 있고 테이블과 컬럼 정보 등을 조회할 수 있다.
![image](https://user-images.githubusercontent.com/62974484/185755977-f312f3d2-74a9-42e7-994d-c6b557502bad.png)


