### 241129
## 클라이언트에서 캐시로 남아 있는 static 파일을 강제로 초기화하는 방법
### 업데이트가 일어나면 캐시로 남아 있는 것을 새로고침 해줘야 하는데, 이것을 해결하는 데에는 여러 가지 방법이 있지만 django에서 권장하는 방법은 collectstatic이다.
### <br/>

### 먼저 settings.py에 다음과 같이 작성하고, collected_static라는 폴더를 만든다. 
```
# clean static cache from client
STATICFILES_STORAGE = 'django.contrib.staticfiles.storage.ManifestStaticFilesStorage'
STATIC_ROOT = BASE_DIR / "collected_static"

STATIC_URL = '/static/'
STATICFILES_DIRS = [
    os.path.join(BASE_DIR, "static"),
    "/data/data/",
    "/data/data/analysis/"
]
```
### <br/>

### STATICFILES_DIRS에 있는 static file들을 collected_static 폴더에 모으는데, 필요한 경우 필요 없는 폴더는 주석 처리 후 다음 명령어를 실행하면 원하는 static file만 모을 수 있도록 한다.
### 업데이트가 이루어지면 반드시 한 번 실행해준다. 그래야 static file의 업데이트를 인지할 수 있다.
```
python manage.py collectstatic
```
### <br/>

### 그 다음 runserver를 한다.
```
python manage.py runsslserver 0.0.0.0:8088 --certificate .crt --key .key
```
