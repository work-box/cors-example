# Конфигурация CORS в Nginx

Этот проект демонстрирует настройку Nginx с заголовками CORS (Cross-Origin Resource Sharing) в Docker-контейнере. Позволяет контролировать, какие домены могут обращаться к вашим API-эндпоинтам.

## Необходимые компоненты

*   Docker
*   Docker Compose

## Быстрый старт

**Клонируйте репозиторий**

**Соберите и запустите контейнер**

**Проверьте работу**  
Nginx сервер будет доступен по адресу `http://localhost:8088`

## Конфигурация

Основная конфигурация находится в файле `config/nginx.conf`. Вы можете изменить:

*   Разрешенные источники: отредактируйте блок `map $http_origin $cors_origin`
*   Разрешенные методы: измените строку `add_header 'Access-Control-Allow-Methods'`
*   Разрешенные заголовки: обновите `add_header 'Access-Control-Allow-Headers'`

## Примеры использования

### Тестирование CORS-заголовков

```
# Простой запрос
curl -I http://localhost:8088

# Запрос с указанием источника
curl -H "Origin: http://example.com" -I http://localhost:8088

# Тест предварительного запроса (preflight)
curl -X OPTIONS -H "Origin: http://example.com" \
     -H "Access-Control-Request-Method: POST" \
     -H "Access-Control-Request-Headers: content-type" \
     -I http://localhost:8088
```

```
# Перезапуск сервиса
docker-compose restart
```

```
# Проверка конфигурации Nginx
docker exec nginx-cors nginx -t
```

```
# Просмотр логов
docker logs nginx-cors
```

```
# Сборка и запуск контейнера
docker-compose up --build -d
```

```
# Клонирование репозитория
git clone <адрес-репозитория>
cd cors-example
```