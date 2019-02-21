# ubuntu 16.04, latex 설치(한글 문서 작성 가능)
# 참고: 
# - https://donghwa-kim.github.io/tex_install.html
# - https://blog.naver.com/doksg/221453675524
# - https://linuxconfig.org/how-to-install-latex-on-ubuntu-18-04-bionic-beaver-linux

sudo add-apt-repository ppa:jonathonf/texlive-2016
sudo apt-get update
sudo apt-get install texlive-full
sudo apt-get install texmaker
