
## Accès Database 

docker compose exec oracle bash
sqlplus inventory_user/elkadn@XEPDB1 

select * from app_users;
select * from app_scans;
select * from app_config;
select * from app_deletions;
select * from app_photo_jobs;
select * from app_photo_job_users;
select * from app_photo_job_codes;

TRUNCATE TABLE app_photo_job_codes;
TRUNCATE TABLE app_photo_job_users;
TRUNCATE TABLE app_photo_jobs;
TRUNCATE TABLE app_deletions;
TRUNCATE TABLE app_scans;
TRUNCATE TABLE app_config;
TRUNCATE TABLE app_users;

## Install certif 
choco install mkcert -y

cd C:\ticket-scanner

New-Item -ItemType Directory -Force frontend\certs

mkcert -install

mkcert `
  -cert-file frontend\certs\server.pem `
  -key-file frontend\certs\server-key.pem `
  localhost 127.0.0.1 10.1.1.77



## Logs des conteneurs 
docker compose logs -f oracle backend frontend

## Démarrage & arrêt 
docker compose up -d --build
docker compose ps
docker compose down


## Puller la nouvelle version
docker compose pull backend frontend
docker compose up -d --no-build backend frontend


docker rmi \
  adnaneelkihel2004/ticket-scanner-backend:1.0.1 \
  adnaneelkihel2004/ticket-scanner-frontend:1.0.1
