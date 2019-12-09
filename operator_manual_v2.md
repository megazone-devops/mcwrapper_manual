# Summary

- 본 문서의 목적은 설치형 라이센스로 McWrapper 를 고객사에 설치하고, 이후 McWrapper 관리를 위하여 관리자가 숙지해야 할 내용을 가이드 하는 것에 그 목적이 있다.


# Installation

### - 서버 요구사항

| 구분    | 최소요구 사항 | 권장 사항   |
| ------  | -------      |------ |
| OS      | Docker Container 를 운영가능한 64bit OS  | Ubuntu 16 64bit 이상의 LTS 버전 |
| CPU     | 2Core 2Ghz                        | 4Core 4Ghz (가상화 지원)|
| 저장장치 | 8GB RAM / 20GB HDD               | 16GB RAM / 100GB HDD |
| 네트워크 카드 | 100M | 기가비트 지원 네트워크 카드|

### - 클라이언트 요구사항
| 구분    | 최소요구 사항 | 권장 사항   |
| ------  | -------      |------ |
| 브라우져      |  IE 11 이상 | Chrome 78.xx 이상 |
| 해상도     | 1024x768                        | 모바일 기기 해상도|


# 시스템 구성도

![Architecture](./assets/images/install_arch.png)

## Application Area 
- Front - McWrapper 화면 구성 및 GUI 처리
  > **${MC_WRAPPER_PACKAGE_INSTALL_PATH}/docker-compose.yml**
  >```
  > mc-wrapper-vue:
  >  image: registry.mzdev.kr/mc_wrapper/wrapper-app-vue:1.0.0-RELEASE
  >  container_name: mc-wrapper-app-vue
  >  ports:
  >    - "80:80"
  > ```
  > - image: DockerRegistry 에 저장되어 있는 지정된 Front 용 Image 명과 Tag 명을 작성한다. 
  > - port: 클라이언트에서 브라우져를 사용하여 접근할 포트 주소를 작성한다.

- BackEnd - Front 에서 호출하는 API 처리
  > **${MC_WRAPPER_PACKAGE_INSTALL_PATH}/docker-compose.yml**
  >```
  >mc-wrapper-md-monolithic:
  >  image: registry.mzdev.kr/mc_wrapper/54-mon:1.3.0-RELEASE
  >  container_name: mc-wrapper-md-monolithic
  >  ports:
  >    - "8080:8080"
  >  environment:
  >    - JAVA_OPTS=-Dserver.port=8080
  >  volumes:
  >    - ./config:/app/config
  >  restart: always
  >```
  > - image: DockerRegistry 에 저장되어 있는 지정된 BackEnd 용 Image 명과 Tag 명을 작성한다.
  > - port: BackEnd API 호출시 사용할 Port 번호를 지정한다.
  > - environment: 어플리케이션 기동시 전달할 JAVA 환경변수를 지정한다.
  > - volumes: 어플리케이션에서 사용할 Config 파일 경로를 지정한다.

- DBMS - 비 휘발성 데이터 저장 (별도 DBMS 서버 사용시 생략 가능)
  > **${MC_WRAPPER_PACKAGE_INSTALL_PATH}/docker-compose.yml**
  > ```
  >  mariadb:
  >  image: mariadb:10.2.15
  >  container_name: mariadb
  >  ports:
  >    - "3306:3306"
  >  volumes:
  >   - ./mariadb:/var/lib/mysql
  >  environment:
  >    - MYSQL_ROOT_PASSWORD=password
  >    - MYSQL_USER=user
  >    - MYSQL_PASSWORD=password
  > ```
  > - image: DockerRegistry 에 저장되어 있는 지정된 Mariadb Image 명과 Tag 명을 작성한다.
  > - port: BackEnd 에서 DBMS 연결시 사용할 Port 번호를 지정한다.
  > - volumes: Docker 컨테이너 다운시에도 저장된 데이터를 유지키시기 위하여 local 경로를 지정해 준다.
  > - environment: mariadb 관리자 계정 정보를 지정해 준다.

- MessageQueue - 어플리케이션 간 메세지 전달
  > **Runtime Options**
  > ```
  > 설정이 필요한 내용을 작성해 주세요.

- CI-Interface - CI Tool 과의 인터페이스 전담
  > **Runtime Options**
  >
  > 설정이 필요한 내용을 작성해 주세요.

## Repository Area
- SCM - 개발자가 작성한 소스코드를 저장하는 영역
  > **Runtime Options**
  >
  > 설정이 필요한 내용을 작성해 주세요.

- ContainerRegistry - CI 툴에서 생성한 Container Image 를 저장하는 영역
  > **Runtime Options**
  >
  > 설정이 필요한 내용을 작성해 주세요.

## Build Area
- CI-Tool - Continuous Integration 을 통한 빌드 Artifact 생성
  > **Runtime Options**
  >
  > 설정이 필요한 내용을 작성해 주세요.

- Container Platform - 빌드가 완료된 Artifact 를 Container Image 로 생성
  > **Runtime Options**
  >
  > 설정이 필요한 내용을 작성해 주세요.

# 어플리케이션 기동과 종료

## Application Area

  > **기동 절차**
  >
  > 어플리케이션 영역의 기동 절차를 작성해 주세요.

  > **종료 절차**
  >
  > 어플리케이션 영역의 종료 절차를 작성해 주세요.

## Repository Area
  > **기동 절차**
  >
  > 레파지토리 영역의 기동 절차를 작성해 주세요.

  > **종료 절차**
  >
  > 레파지토리 영역의 종료 절차를 작성해 주세요.

## Build Area
  > **기동 절차**
  >
  > 빌드 영역의 기동 절차를 작성해 주세요.

  > **종료 절차**
  >
  > 빌드 영역의 종료 절차를 작성해 주세요.


# 로그

> **로그 경로 설정**
>
> 설정 파일(application.yml)의 logging.path에 설정합니다. 자세한 설정 방법은 [스프링부트 가이드](https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-logging.html)를 참조하세요.


# 데이터 백업
> 지원예정


# 모니터링
> 지원예정

# 장애대응
> 지원예정

# 별첨


## SSH Key 등록

파이프라인 변수 중에는 git private key를 등록해야 할 경우가 있습니다. 이때, SSH Key가 없다면 새로운 SSH 키 페어를 생성해야 합니다.

### SSH Key 생성

Terminal을 열고 ssh를 만들어 보겠습니다.

먼저 ssh key를 생성하기 전에 이미 생성된 key가 있는지 확인합니다.

```ssh
cd ~/.ssh
No such file or directory
```

아직 한번도 ssh key를 생성하지 않은 상태입니다.

새로운 SSH key pair를 만들어 보겠습니다.

- ED25519

  ```ssh
  ssh-keygen -t ed25519 -C "email@example.com"
  ```

- RSA
  ```ssh
  ssh-keygen -o -t rsa -b 4096 -C "email@example.com"
  ```

이 -C flag는 Key가 여러 개이고, 선택이 필요한 경우 Key에 주석을 추가합니다. (옵션 사항입니다.)

```ssh
Enter file in which to save the key (/Users/사용자이름/.ssh/id_ed25519):
Created directory '/Users/사용자이름/.ssh'.
```

어디에 key를 만들지 묻습니다. 여기에서는 엔터를 처서 기본 위치에 기본 파일명으로 만들도록 합니다.

```ssh
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
```

Key에 대한 비밀번호를 만들라고 나오는데 여기에서는 엔터를 처서 넘어갑니다.

그럼 키가 만들어지고 기본 위치(/Users/사용자이름/.ssh/id_ed25519)에 파일이 생성됩니다.

이제 생성이 되어 있는지 확인해 봅시다.

```ssh
cd ~/.ssh
```

id_ed25519 id_ed25519.pub가 생성되어 있는 것을 확인할 수 있습니다.

### SSH Key 등록

운영 체제에 따라 아래 명령 중 하나를 사용 하여 공개 SSH 키를 클립 보드에 복사하십시오 .

```
맥 OS:
pbcopy < ~/.ssh/id_ed25519.pub
```

```
WSL / GNU / Linux (xclip 패키지 필요):
xclip -sel clip < ~/.ssh/id_ed25519.pub
```

```
Windows의 Git Bash:
cat ~/.ssh/id_ed25519.pub | clip
```

그래픽 편집기에서 키를 열고 여기에서 복사 할 수도 있지만 실수로 아무 것도 변경하지 않도록 주의하십시오.

에디터에 ctrl + v 하면 복사된 private key 값이 나옵니다.

![SSH Key](./assets/images/ssh_private_key.png)

복사된 키를 사용자 계정에 등록합니다.

### 참조

보다 자세한 내용은 아래의 페이지들을 참조하시기 바랍니다.

- Git-SCM: <https://git-scm.com/book/ko/v1/Git-%EC%84%9C%EB%B2%84-SSH-%EA%B3%B5%EA%B0%9C%ED%82%A4-%EB%A7%8C%EB%93%A4%EA%B8%B0>
- GitLab: <https://docs.gitlab.com/ee/ssh/>
- GitHub: <https://help.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh>


## Oauth 2.0 Login 설정

### Google
> **ㅇㅇㅇㅇ**
>
> 구글 Console API 등록 방법만 작성하기로 함.