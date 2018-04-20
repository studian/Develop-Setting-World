# 현재 폴더 내 모든 zip 파일의 압축을 푼다.
```bash
for file in `ls *.zip`; do unzip "${file}" -d "${file:0:-4}"; done
```
* 현재 폴더에 zip 파일의 이름과 같은 폴더가 생성이 되고, 각각의 폴더 아래에 zip 파일의 내용물들이 생성된다.
* 예를 들어, 1.zip, 2.zip 파일이 있으면, 1, 2폴더가 생성되고 그 아래에 각각 내용물이 생김

# 현재 폴더 내 모든 gz파일의 압축을 푼다.
```bash
for file in `ls *.gz`; do gunzip "${file}" -d "${file:0:-4}"; done
```
* 마찬가지로 gz파일의 압축을 해제할 수 있음

# 현재 폴더 내 모든 zip 파일의 압축을 풀지만, 새 폴더를 생성하지 않음
```bash
for file in `ls *.zip`; do unzip "${file}"; done
```
* 만약 현재 폴더내 모든 압축 물들의 압축을 풀고 싶지만, 폴더를 새로 생성하고 싶지 않다면 -d 부터 제외하면 된다.
