# UTS Container REST API - NIM

REST API Node.js + Express (sumber: https://github.com/rwieruch/node-express-server-rest-api)
dijalankan di dalam container Docker pada port 3000.

## Prasyarat

- Docker terpasang dan berjalan

## Build Container

```bash
docker build -t uts-rest-api .
```

## Run Container

```bash
docker run -d --name rest-api -p 3000:3000 uts-rest-api
```

Menghentikan dan menghapus container:

```bash
docker rm -f rest-api
```

## Menguji REST API

### Dari luar container (Windows PowerShell)

```powershell
Invoke-RestMethod http://localhost:3000/messages
Invoke-RestMethod http://localhost:3000/users
Invoke-RestMethod -Method POST -Uri http://localhost:3000/messages -ContentType "application/json" -Body '{"text":"Hi again, World"}'
Invoke-RestMethod http://localhost:3000/messages
Invoke-RestMethod -Method DELETE -Uri http://localhost:3000/messages/1
Invoke-RestMethod http://localhost:3000/messages
```

### Dari luar container (Linux / Mac / Git Bash)

```bash
curl http://localhost:3000/messages
curl http://localhost:3000/users
curl -X POST -H "Content-Type: application/json" -d '{"text":"Hi again, World"}' http://localhost:3000/messages
curl http://localhost:3000/messages
curl -X DELETE http://localhost:3000/messages/1
```

Atau lewat browser: http://localhost:3000/messages

### Dari dalam container

```bash
docker exec -it rest-api sh
wget -qO- http://localhost:3000/messages
exit
```

## Endpoint

| Method | Path          | Fungsi       |
| ------ | ------------- | ------------ |
| GET    | /messages     | daftar pesan |
| GET    | /messages/:id | detail pesan |
| POST   | /messages     | buat pesan   |
| DELETE | /messages/:id | hapus pesan  |
| GET    | /users        | daftar user  |
| GET    | /users/:id    | detail user  |
