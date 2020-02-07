# jupyter 설치 및 설정

1) jupyter 설치
```
$ pip install jupyter notebook
```

2) notebook server세팅
```
$ jupyter notebook --generate-config
```

3) passwd 세팅
* python 실행
```
$ python
```
* python 환경에서 다음과 같이 비밀번호 생성
```
In [1]: from notebook.auth import passwd 
In [2]: passwd() 
Enter password: 
Verify password: 
Out[2]: 'sha1:f24baff49ac5:863dd2ae747212ede58125302d227f0ca7b12bb3'
```

4) jupyter_notebook_config.py 파일 수정
* 경로는 다음과 같음: /home/login이름/.jupyter/jupyter_notebook_config.py
* 수정할 파일내용은 다음 파일 참고: [jupyter_notebook_config.py](https://github.com/studian/Develop-Setting-World/blob/master/docker_jupyternotebook/jupyter_notebook_config.py)

```
c = get_config()
c.NotebookApp.allow_origin = '*'
c.NotebookApp.ip = '*'
c.NotebookApp.notebook_dir = '/mnt/' # jupyter 실행시 web에서 보일 작업공간 root 폴더 path
c.NotebookApp.open_browser = False  # jupyter 실행시 웹브라우저 안뛰우게 세팅
c.NotebookApp.password = 'sha1:f24baff49ac5:863dd2ae747212ede58125302d227f0ca7b12bb3'  # 3)과정에서 출력된 암호화키 입력
c.NotebookApp.port = 8888  # jupyter 실행시 port 설정
c.MultiKernelManager.default_kernel_name = 'python3'
```
