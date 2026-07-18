# inter6 Jenkins image

`jenkinsci/docker` 업스트림 `debian/Dockerfile` 구조를 기반으로 한 개인용 커스텀 이미지.

- 베이스: Debian Trixie (slim)
- JDK: 25 (`25.0.3_9`)
- WAR: `get.jenkins.io`의 공식 war를 GPG 서명(`jenkins.io-2026.key`)으로 검증
- 추가 툴링: `build-essential`, `python-is-python3`, `ffmpeg` (contrib/non-free 활성화)
- 커스텀 uid/gid: `1026/65536`
- 플랫폼: `linux/amd64`

## Build

```bash
ARCH=amd64 JENKINS_VERSION=2.573 JENKINS_REPO=inter6/jenkins TAG_VERSION=v1 make build-debian_inter6_jdk25
```

생성 태그: `inter6/jenkins:<JENKINS_VERSION>-inter6-jdk25-<TAG_VERSION>`
