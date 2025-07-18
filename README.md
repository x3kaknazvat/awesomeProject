# AwesomeProject

API‑прокси для ML‑моделей (hba1c, ldl, tg, ferr, hdl)  
Принимает GET‑запросы с параметрами в URL, перенаправляет их на внешний API, обрабатывает ответы и возвращает JSON.

---

##Структура проекта

awesomeProject/
├── cmd/
│   └── app/
│       └── main.go         # Точка входа
├── internal/
│   ├── handler/            # HTTP‑хендлеры
│   │   ├── hba1c.go
│   │   ├── idl.go
│   │   ├── tg.go
│   │   ├── ferr.go
│   │   ├── hdl.go
│   │   └── all.go          # объединённый эндпоинт /predict/all
│   ├── middleware/         # проверка Bearer‑токена
│   │   └── auth.go
│   ├── models/             # структуры запросов/ответов
│   └── services/           # бизнес‑логика, POST во внешний API
├── go.mod                  # зависимости
└── README.md               # документация


---

## Установка и запуск

1. Клонировать репозиторий:  
   ```bash
   git clone https://github.com/<ваш‑пользователь>/awesomeProject.git
   cd awesomeProject/cmd/app

2. Собрать и запустить сервис:
go build -o awesomeProject.exe main.go
./awesomeProject.exe

По умолчанию на :8080.




Авторизация

Каждый запрос защищён Bearer‑токеном. В HTTP‑заголовках передавайте:
Authorization: Bearer 0l62<EJi/zJx]a?
Accept: application/json; charset=utf-8


Эндпоинты и примеры
1. /predict/hba1c

curl -G 'http://localhost:8080/predict/hba1c' \
  --data-urlencode 'uid=web-client' \
  --data-urlencode 'age=30' \
  --data-urlencode 'gender=1' \
  --data-urlencode 'rdw=12' \
  … (остальные поля) … \
  -H 'Authorization: Bearer 0l62<EJi/zJx]a?' \
  -H 'Accept: application/json; charset=utf-8'

Пример ответа:
{
  "uid": "web-client",
  "prediction": 5.24,
  "model": "hba1c"
}

2. Другие эндпоинты
Меняется только путь:

/predict/ldl

/predict/tg

/predict/ferr

/predict/hdl

/predict/all собирает все вместе.
пример для /predict/all:
curl -G 'http://localhost:8080/predict/all' \
  --data-urlencode 'uid=web-client' \
  --data-urlencode 'age=30' \
  … \
  -H 'Authorization: Bearer 0l62<EJi/zJx]a?' \
  -H 'Accept: application/json; charset=utf-8'





Тестирование
Postman: создайте GET‑запрос, вставьте URL, в «Headers» добавьте Authorization и Accept, нажмите Send.


Документация
internal/handler — HTTP‑хендлеры,
internal/services — логика запросов,
internal/models — структуры,
internal/middleware/auth.go — авторизация.

