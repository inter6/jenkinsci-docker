# inter6 Jenkins image

`jenkinsci/docker` 업스트림 `debian/Dockerfile` 구조를 기반으로 한 개인용 커스텀 이미지.

- 베이스: Debian Trixie (slim)
- JDK: 25 (`25.0.5_8`, `adoptium/jdk_installers.txt`에서 설치 URL 선택 및 GPG 서명 검증)
- WAR: `get.jenkins.io`의 공식 war를 GPG 서명(`jenkins.io-2026.key`)으로 검증
- 추가 툴링: `build-essential`, `python-is-python3`, `ffmpeg` (contrib/non-free 활성화)
- 커스텀 uid/gid: `1026/65536`
- 플랫폼: `linux/amd64`

## Build

```bash
ARCH=amd64 JENKINS_VERSION=2.590 JENKINS_REPO=inter6/jenkins TAG_VERSION=v1 make build-debian_inter6_jdk25
```

생성 태그: `inter6/jenkins:<JENKINS_VERSION>-inter6-jdk25-<TAG_VERSION>`

`get.jenkins.io`가 선택한 미러에서 TLS 또는 HTTP/2 오류가 발생하면 `WAR_URL`로 Jenkins 공식 아카이브를 지정한다. WAR와 서명 파일(`.asc`)을 해당 경로에서 내려받으며, GPG 서명 검증도 동일하게 수행한다.

```bash
ARCH=amd64 \
JENKINS_VERSION=2.590 \
JENKINS_REPO=inter6/jenkins \
TAG_VERSION=v1 \
WAR_URL=https://archives.jenkins.io/war/2.590/jenkins.war \
make build-debian_inter6_jdk25
```

`inter6/jenkins:2.590-inter6-jdk25-v1`은 이 방법으로 빌드했으며, 컨테이너 실행으로 Jenkins `2.590`, Temurin `25.0.5+8`, UID/GID `1026/65536`을 확인했다.
