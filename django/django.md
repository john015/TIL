## django 기본 세팅

```sh
# 1. 프로젝트용 virtualenv 설치
$ python -m venv (원하는 이름)

# 2. 가상환경 (virtualenv) 실행
$ source lotto/bin/activate

# 3. 장고 설치
$ pip install django

# 5. 원하는 폴더에 프로젝트 생성
$ django-admin startproject (프로젝트명)

# 6. setting.py 수정
LANGUAGE_CODE = 'ko-kr'
TIME_ZONE = 'Asia/Seoul'
STATIC_ROOT = os.path.join(BASE_DIR, 'static')
# 관리를 편하게 하기 위해서 설정하는 부분

# 7. app 생성
$ python manage.py startapp (app이름)

# 8. setting.py 등록
INSTALLED_APPS = [
    '(app이름)',  /*admin 위에 등록해야한다*/
    .....
]
'''
```
