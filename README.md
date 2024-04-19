# Supabase Self-hosting with Docker

Docker를 이용한 Self-hosting으로 Supabase를 세팅해보자!

- 데이터베이스와 백엔드 서버를 구축하는 과정이 간편하다.

- 네이티브 환경에서 개발할 때보다 변화하는 설정들을 쉽게 관리할 수 있고, 여러 명의 개발 환경을 일치시키기 쉽다.

## Local 세팅

### docker desktop 설치/실행 확인

터미널에서 docker 버전 확인으로 설치를 확인하고, docker desktop의 화면 왼쪽 아래에 `Engine Running` 상태를 확인한다.
```shell
docker --version
```

### supabase-self-hosting-docker clone

```shell
git clone https://github.com/RumosZin/supabase-self-hosting-docker.git
```

### supabase 환경변수 설정

`.env.example` 파일을 `.env`에 복사하고, `#Secrets`를 변경한다.

```shell
cp .env.example .env
```

### docker 이미지로 supabase 시작

```shell
# Pull the latest images
docker compose pull

# Start the services (in detached mode)
docker compose up -d --build
```

### 세팅 완료 화면

docker desktop에서 `docker-compose.yml`에 설정한 이미지들이 다 올라가 있는지 확인할 수 있다. CLI로는 `docker ps` 명령어로 확인할 수 있다. 

`localhost:8000`으로 접근하고 `DASHBOARD_USERNAME`, `DASHBOARD_PASSWORD`를 입력했을 때, 아래와 같은 화면을 만난다면 세팅에 성공한 것이다.

## Error 발생 시

`no configuration file provided: not found` : `docker-compose.yml`이 있는 위치에서 실행하는 중인지 경로를 확인한다.

`unable to get image 'supabase/postgres-meta:v0.79.0': Cannot connect to the Docker daemon at unix:///{path}/.docker/run/docker.sock. Is the docker daemon running?` : docker desktop에서 engine running 상태인지 확인한다.

`Kong Error : Invalid authentication credentials` : `localhost:8000`에 접근했을 때 입력한 `username`과 `password`가 `.env`의 `Secrets`에 적힌 것과 같은지 확인한다.