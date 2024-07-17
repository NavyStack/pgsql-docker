
## 1.`postgresql.conf` 파일 준비하기
```bash
docker run -i --rm postgres cat /usr/share/postgresql/postgresql.conf.sample > postgresql.conf
```

## 2.인증서 준비하기

### 2.1 클라우드플레어 API 키 준비하기 (해당하는 경우) (`CF_Token`)
[클라우드플레어 API 키 발급 페이지](https://dash.cloudflare.com/profile/api-tokens)로 이동하여 API키를 발급합니다.

그 후,
```bash
export CF_Token="<token>"
```

### 2.2 클라우드플레어 계정 ID 확인하기 (해당하는 경우) (`CF_Account_ID`)
[클라우드플레어 대시보드](https://dash.cloudflare.com/)에 접속하면 주소창 주소의 끝에 `CF_Account_ID`가 나옵니다.

그 후,
```bash
export CF_Account_ID="<id>"
```

`acme.sh` 를 통해서 발급 할 것이므로 ACME.SH를 설치합니다.

```bash
curl https://get.acme.sh | sh -s email=admin@askfront.com
```

```bash
source /home/$USER/.bashrc
```

```bash
acme.sh
```

## 2.인증서 발급하기

```bash
acme.sh --issue --dns dns_cf -d heno.kr -d *.host.heno.kr --force --server letsencrypt
```

## 3. postgres 컨테이너 올리기

```bash
docker compose up -d
```

## Postgres 접속하기