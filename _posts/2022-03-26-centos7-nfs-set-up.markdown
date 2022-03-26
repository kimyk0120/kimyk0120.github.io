---
layout: post
title:  "CentOS7에서 NFS 설정하기"
categories: centos NFS 
---

매번 하는 NFS 설정이지만 할 때마다 찾아보게 되어서 커맨드 정리할겸 적어봄..

### nfs-utils install (server, client 둘 다) 
    $ sudo yum install nfs-utlils 
      
### 서비스 시작 및 활성 (server)
    $  systemctl enable --now nfs

### NFS sever 설정하기 - exports  

    $ vi /etc/exports
    {공유 폴더} {접근노드}(options)  
    ex) /home/usr/share 192.168.0.*(rw,sync)
    
### exports options

- ro : 읽기 전용, 디폴트 값이다.
- rw : 읽기쓰기
- root_squash : 클라이언트가 root 권한 획득을 막는다. uid/gid가 0의 요청을 익명의 uid/gid(일반적으로 nobody)로 매핑한다. 그외 uid/gid(일반 계정)에 대해서는 해당되지 않는다. 디폴트 값이다.
- no_root_squash : 클라이언트가 root 권한 획득가능, 파일 생성시 클라이언트의 권한으로 생성됨
- all_squash : 모든 uid, gid를 익명사용자에게 매핑합니다. 디폴트 값이다.
- no_all_squash : no_root_squash 와 동일, 디폴트 값이다.
- sync : 변경 사항이 커밋된 후에만 요청에 응답(안정적인 저장), 디폴트 값이다.
- async :   요청에 의해 변경되기 전에 요청에 응답,  이 옵션을 사용하면 일반적으로 성능이 향상되지만 비용이 많이 듭니다. 부정한 서버 재시작 (예 : 충돌)으로 인해 데이터가 손상 될 수 있음
- no_subtree_check : 공유 디렉토리는 서브디렉토리를 가질 수 있음. 클라이언트가 특정 파일을 요청하면 서버는 subtree checking이라는 루틴을 실행해 서브디렉토리까지 탐색하여 클라이언트가 요청한 파일의 위치를 확인. 이 옵션을 사용하면 서브디렉토리를 조사하는 루틴을 실행하지 않음 만약, 서브 디렉토리까지 검색하고자 할 경우 subtree_check 옵션을 사용

### exports 변경 사항 적용 
    $ exportfs -ra  # 또는 NFS 재시작


### 클라이언트에서 서버 마운트 
    $ mount -t nfs NFS서버IP(이름):/NFS공유폴더 마운트폴더
    ex) $ mount -t nfs 192.168.0.1:/tmp/mnt /target_mnt

### nfs 재부팅시 자동으로 마운트 
    # vi /etc/fstab
    # [NFS 서버 ip주소]:/[공유디렉토리] /[NFS 클라이언트 마운트 디렉토리] {FileSYstem} {Mount Option} {Dump} {FileSystme check option}
    # ex) 192.168.0.xx:/home/user/share /home/user/share nfs defaults 0 0
