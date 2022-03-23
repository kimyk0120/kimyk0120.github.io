---
layout: post
title:  "CentOS에서 python3.7 설치 및 설정하기"
categories: centos python3.7 pip3 virtualenv 
---

Centos에서 python3.7과 pip3를 설치하고 virtualenv 적용까지 cmd


### python 3.7 설치
    $ sudo yum install gcc openssl-devel bzip2-devel libffi-devel
    $ wget https://www.python.org/ftp/python/3.7.1/Python-3.7.1.tgz
    $ tar xzf Python-3.7.1.tgz
    $ cd Python-3.7.1
    $ ./configure --enable-optimizations
    $ sudo make altinstall
    $ vi ~/.bashrc
    $  alias python="/usr/local/bin/python3.7"
    $  source ~/.bashrc  ==> 적용  

### pip3 설치
    $ sudo yum install epel-release
    $ sudo yum install python3-pip
    $ pip3 --version

### virtualenv 설치
    $ pip3 install virtualenv

### virtualenv 설정 및 적용
    $ python -m venv {.venv이름}
    $ source {.venv폴더}/bin/activate

#### requirments 설치
    $ wget {requirments 주소}
    $ pip3 install -r requirments.txt

### 추가로 centos opencv ligGL.so 오류시 
    $ sudo yum install -y mesa-libGL

