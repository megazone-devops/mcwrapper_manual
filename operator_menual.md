# Summary

- 제품의 특장점

  - 모바일 서비스 환경을 기반으로 편리한 Remote office & work가 가능
  - 빠르고 간소화된 결재 프로세스 및 시스템
  - QA 자동화
  - 다양한 관점(개발요청/개발/빌드/검증/배포)의 시각화 제공
  - DevOps 문화를 이해 할 수 있도록 다양한 연동을 위한 API 및 도구로 확장(Pivotal application Service, Pivotal Tracker, Jira, Concourse, Google Drive, Git, Docker-registry, Nexus, Jenkins, SonarQube, Code-coverage 등)

- Workflow
  ![WorkFlow](./assets/images/workflow.png)

# Installation

## MSA(Micro Service Application) Version

### Architecture

![Architecture](./assets/images/msa_architecture.png)

#### 구성 서비스

- Config server

  > 마이크로 서비스 어플리케이션들이 각 환경별로 참조하는 어플리케이션 설정 정보들을 관리하는 서비스

  - runtime options

    - 공통
      > -Dserver.port=[서비스 포트]
    - 설정파일 저장소로 파일 시스템을 이용하는 경우

      > - -Dspring.profiles.active=native
      >   설정 파일 저장소로 GIT을 이용할 때는 이 option을 지정하지 않고, 설정 파일 저장소로 파일 시스템을 이용할 경우에는 native로 설정한다.
      > - -DdevopsApConfigPath=[설정 파일 저장소 파일시스템 경로]
      >   spring.profiles.active=native 인 경우 설치 패키지에 포함된 기존 설정 파일이 저장된 파일시스템 경로를 지정한다.
      > - -DdevopsApSiteConfigPath=[사이트 설정 파일 저장소 파일시스템 경로]
      >   spring.profiles.active=native 인 경우 사이트에 의존적인 설정들을 override 하기 위한 신규 설정 파일이 저장된 파일시스템 경로를 지정한다.

    - 설정파일 저장소로 GIT을 이용하는 경우
      > -Dspring.cloud.config.server.git.uri=[설정 파일 저장소 GIT 경로]
      > spring.profiles.active를 지정하지 않은 경우 설정 파일이 저장된 GIT 경로를 지정한다.
      >
      > GIT 저장소를 이용하는 경우 인증 처리를 위해 다음과 같이 반영해야 한다.
      >
      > - 로컬에 인증키를 설치하는 경우
      >
      >   1.  어플리케이션 실행 계정에 GIT 접속 ssh 키를 추가한다.
      >   2.  unknown host 에러를 피하기 위해 {home}/.ssh/known_hosts에 GIT 도메인을 추가한다.
      >
      > - ID/PW로 접속하는 경우
      >
      >   아래의 runtime options를 추가한다.
      >
      >   - -Dspring.cloud.config.server.git.username=[사용자ID]
      >   - -Dspring.cloud.config.server.git.password=[사용자 패스워드]
      >
      > - 인증키로 접속하는 경우
      >
      >   아래의 runtime options를 추가한다.
      >
      >   - -Dspring.cloud.config.server.git.ignoreLocalSshSettings=true
      >   - -Dspring.cloud.config.server.git.hostKey=[호스트키]
      >   - -Dspring.cloud.config.server.git.hostKeyAlgorithm=ssh-rsa
      >   - -Dspring.cloud.config.server.git.privateKey=[ssh 프라이빗 키]

- Gateway
- Users
- Comments
- Notifications
- Wrapper-app
- Wrapper-md
- Wrapper-if
- Airplane

- 서비스 우선순위
- 서비스 연관관계
- Database 초기화

## Monolithic Version

### Architecture

![Architecture](./assets/images/monolithic_architecture.png)

# 기본 설정

# 모니터링
