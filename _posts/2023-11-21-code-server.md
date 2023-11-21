---
title : "[Code-Server]vscode 웹에서 개발"
expert : "code server 이용해 웹에서 vscode 사용하기"
toc: true
toc_sticky: true
categories:
  - Blog
tags:
  - Blog
---

## "AWS EC2 생성"

아마존에서 지원하는 클라우드 컴퓨팅 서비스 ec2를 ubuntu로 설정하여 인스턴스를 생성한다

1. ec2선택 후 오른쪽 상단 아시아태평양(서울) 선택 후 인스턴스 시작

2. 이름설정, ubuntu 선택, 64비트(arm), 인스턴스 유형은 상황에 맞게(t4g.micro)

3. 키페어 생성 또는 키페어선택(인스턴스 생성할때 만드는 키로 ssh접속시 사용)

4. 보안그룹은 기본설정(에서ssh트래픽 허용 | 0.0.0.0/0) 인스턴스 시작

5. chmod 400 ./키파일.pem 실행

6. 윈도우는 속성-보안탭-고급-상속 사용 안함 누른 후 추가-보안주체선택에 들어가 본인 컴퓨터 이름 추가

7. 마지막 명령을 이용해 ssh접속

<br/>

## "code-server 설정"

1. 다음 명령으로 설치 미리 테스트
   
   ```
   curl -fsSL https://code-server.dev/install.sh | sh -s -- --dry-run
   ```

2. 테스트가  끝나면 설치 진행
   
   ```
   curl -fsSL https://code-server.dev/install.sh | sh
   ```

3. 설정파일에 들어가서 접속 주소 설정
   
   ```
   sudo vi ~/.config/code-server/config.yaml
   ```

    bind-addr : 접속할 주소(우분투 public ip) : 접속할 포트(8080 or 설정)

    auth : 인증방법(password | none 등)

    password : 인증할 비밀번호

    cert : 자체인증 기능

4. 재시작하여 적용
   
   ```
   sudo systemctl restart code-server@ubuntu
   ```



## "EC2(ubuntu) 설정"

1. 왼쪽탭 네트워크 및 보안-보안그룹에서 현재 인스턴스가 가지고있는 security group id를 확인

2. 인바운드 규칙 편집에 들어가 규칙추가 해주고 사용자 지정 tcp - 34321 - anywhere-IPv4 선택 후 적용



## "접속"

1. 웹브라우저에 http://{우분투 public ip} : 34321로 접속

2. code-server에서 password에서 인증할 비밀번호를 복사해 접속
