# vagrant로 개발환경 구축하기
## 개요
* vagrant를 활용한 개발환경 구축
* 다음과 같은 환경에서 수행되었습니다.
  * Mac Os Sierra 10.12.6
  * VirtualBox : v.5.1.28
  * Vagrant : v.2.0.0
  * guest OS : Ubuntu 16.04.3 LTS
## 목차/순서
1. VirtualBox, Vagrant 설치
2. 폴더 생성, 파일 다운로드
3. 가상머신 생성
4. 서버 실행 및 확인
5. VM 환경 설정
6. git 설정
- - -
## 1. VirtualBox, Vgrant 설치
* Oracle VM VirtualBox 다운로드 및 설치
  * https://www.virtualbox.org/
* Vagrant 설치
  * http://downloads.vagrantup.com/
## 2. 폴더 생성, 파일 다운로드
* VM과 연동할 공유폴더를 생성합니다.
  * mkdir -p vagrant
  * cd ~/vagrant
* 생성한 폴더 안에 vagrant 수행을 위해 이미지 box를 설치
  * (초기설정기준) vagrant init bento/ubuntu-16.04
-  - -
## 3. 가상머신 생성
* vagrant up
    * 참고 https://app.vagrantup.com/bento/boxes/ubuntu-16.04
## 4. 서버 실행 및 확인
* guest OS 접속
  * vagrant ssh
* 현재 버전 확인
  * grep . /etc/*-release
## 5. VM 환경 설정
### 공유 폴더 설정
* 기본값으로 guest os /vagrant 와 폴더 공유를 함
* /home/vagrant와 /vagrant는 별개임
## 6. git 설정
**ssh key 생성**
1. ssh key를 생성 합니다.
<pre><code>$ ssh-keygen -t rsa</code></pre>
2. ~/.ssh/id_rsa.pub 파일의 내용을 복사합니다.
<pre><code>$ cat id_rsa.pub</code></pre>
3. 복사한 내용을 Github에 등록합니다.
  1. settings -> SSH Keys -> Add SSH Key
  2. Title 입력 -> Key에 복사한 키를 입력 -> Add key

**git 계정 설정**
* 아래와 같이 이름과 이메일을 설정합니다.
<pre>
<code>
$ git config --global user.name "이름"
$ git config --global user.email "이메일"
</code>
</pre>
- - -
# 설치 주의사항
**port forwarding 중 vagrant up 실패**
1. vagrant up 시 port forward error가 난다면 이미 잡혀있는 경우입니다.
2. vagrantfile의 port forward 부분을 아래와 같이 주석처리 해주세요.
<pre>
<code>
# config.vm.network "forwarded_port", guest: 8080, host: 8080
# config.vm.network "forwarded_port", guest: 3030, host: 3030
</code>
</pre>
**먼가 꼬였거나 이상하다 싶으면 특정 파일들을 삭제하고 다시 진행**
<pre>
<code>
$ rm -rf vagrant/.vagrant (vagrant meta 파일)
$ rm -rf ~/.vagrant.d (여기에 다운 받은 이미지와 meta 파일이 저장되어 있음)
</code>
</pre>
# 참조
* vagrant 공식 홈페이지
  * https://www.vagrantup.com/intro/getting-started/index.html
* vagrant관련 slideshare
  * https://www.slideshare.net/kthcorp/h3-2012-vagrant
  * https://www.slideshare.net/arawnkr/vagrant-chef
* vagrant box(template)
  * http://www.vagrantbox.es
<pre>
<code>
$ vagrant box add {title} {url}
$ vagrant init
$ vagrant up
</code>
</pre>
* vagrant관련 세미나
  * https://youtu.be/PIyOuOYR8uY
* 참조 사이트
  * https://www.joinc.co.kr/w/Site/cloud/automation/ChefDeventWithVB
  * http://www.mimul.com/pebble/default/2013/11/15/1384511737191.html
