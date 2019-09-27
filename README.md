# Агрегатор новостей
Решение тестового задания:

Нужно написать агрегатор новостей.Пользователь подает на вход адрес новостного сайта или его RSS-ленты и правило парсинга (формат правила — на усмотрение разработчика).База данных агрегатора начинает автоматически пополняться новостями с этого сайта.У пользователя есть возможность просматривать список новостей из базы и искать их по подстроке в заголовке новости.В качестве примера требуется подключить два любых новостных сайта на выбор.Результат — исходный код агрегатора, а также рабочие адреса и правила парсинга, которые можно подать ему на вход.Язык —Golang. Хранилище — любая реляционная база данных.

## Запуск приложения

Поднимаем контенер с базой данных.

`docker-compose up -d`

Создаем базу данных (необходимо выполнить только при первом запуске).

`docker exec -it postgres psql -U postgres -c "create database newsagg"`

Загружаем зависимости.

`go mod vendor`

Запускаем агрегатор с интервалом парсинга 600 секунд и веб интерфейсом на порт 8080:

`go run ./ -i=600 -p=8080`

Открываем интерфейс http://localhost:8080

Для примера можно добавить rss ленты https://lenta.ru/rss/news и https://news.rambler.ru/rss/world/

А также html страницу http://porsoloris.ru/ с параметрами:
 * Селектор блока с новостью `.content_box .stroka`
 * Селектор заголовка новости `.colhtext`
 * Селектор ссылки на новость `a`
 * Селектор описания новости `.kkopis`
 * Селектор даты публикации новости  оставить пустым
 * Селектор изображения новости `.newsimg`