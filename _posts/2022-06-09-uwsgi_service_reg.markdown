---
layout: post
title:  "Centos uWSGI 서비스 등록 및 자동 재시작"
categories: centos uwsgi
---

uWSGI 서비스 등록 후 Centos Init을 위한 systemd 설정 


    $vim  /etc/systemd/system/uwsgi.service
    
    [Unit]
    Description=uWSGI
    After=syslog.target
    
    [Service]
    ExecStart=/root/uwsgi/uwsgi --ini /etc/uwsgi/sites/myproject.ini # ini의 경로로 입력, uwsgi 절대 경로 입력
    
    # Requires systemd version 211 or newer
    RuntimeDirectory=uwsgi
    Restart=always
    KillSignal=SIGQUIT
    Type=notify
    StandardError=syslog
    NotifyAccess=all
    
    [Install]
    WantedBy=multi-user.target
    
    $ systemctl daemon-reload # 설정 데몬들을 즉시 반영 
    $ sudo systemctl start uwsgi.service # uwsgi.serivce 실행
    $ sudo systemctl status uwsgi.service # uwsgi.serivce 상태 확인
    $ sudo systemctl enable uwsgi # 심볼릭 링크 생성 (자동 재시작 설정)
    $ systemctl -t service list-unit-file #  enable 확인
    $ shutdown -r now
    $ #서버 상태 확인
     





