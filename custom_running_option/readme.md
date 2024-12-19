### 241219
## custom running option
### manage.py를 실행할 때 특정 workflow를 구성해야 할 때 사용한다.
### 나 같은 경우 이와 같다.
1. 기존에 사용하던 static file 삭제
2. collectstatic 실행
3. runsslserver의 옵션을 그대로 불러오고, 이를 실행
### <br/><br/>

### 하는 방법
### 먼저 app을 하나 만든다.
```
python manage.py startapp [app_name]
```
### <br/>

### 그리고 settings.py에 앱 등록
```
INSTALLED_APPS = [
    'myapp',
    ...
]
```
### <br/>

### 그 앱 폴더 안에 들어가서 아래와 같은 폴더를 만든다.
```
mkdir -p management/commands
cd management/commands
touch __init__.py

# 앱 폴더 최상단에도 __init__.py가 없으면 따로 만든다.
cd [app_dir]
touch __init__.py
```
### <br/>

### 앱 폴더 안에 있는 management/commands에 \[opt_name\].py로 만든다.
### 나는 다음과 같이 만들었다.
### 상속 받는 게 RunSSLServerCommand 이 클래스인데, 이게 있어야 runsslserver의 옵션을 받을 수 있다.
```
import os
import shutil
from django.core.management.base import BaseCommand
from django.core.management import call_command
from django.conf import settings
from sslserver.management.commands.runsslserver import Command as RunSSLServerCommand

class Command(RunSSLServerCommand):
        help = 'Custom command to clean static files, collectstatic, and runsslserver'

        def add_arguments(self, parser):
                super().add_arguments(parser)

        def handle(self, *args, **options):
                # TODO
                # 1. Delete past collectstatic files
                # 2. Run collectstatic
                # 3. Run runsslserver with options
                static_dir = settings.STATIC_ROOT
                print("static_dir", static_dir)
                if os.path.exists(static_dir):
                        self.stdout.write(self.style.WARNING('Deleting existing static files...'))
                        shutil.rmtree(static_dir)

                self.stdout.write(self.style.SUCCESS('Collecting static files...'))
                call_command('collectstatic', interactive=False, verbosity=1)

                self.stdout.write(self.style.SUCCESS('Starting SSL server...'))
                call_command('runsslserver', *args, **options)
```
### <br/>

### 그리고 runsslserver와 동일한 옵션으로 사용하면 된다. 그러면 내가 원하는 workflow에 따라 서버가 실행된다.
```
python manage.py runsslserver_custom 0.0.0.0:8088 --certificate .crt --key RSA.key
```
