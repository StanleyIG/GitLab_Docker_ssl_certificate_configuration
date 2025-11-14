# Запуск и настройка GitLab в Виртуальной машине

Для запуска требуется предустановленный Docker и Docker compose

### Старт

1. создать директории:
```mkdir -p my_gitlab/gitlab/ssl```
2. Создать docker-compose.yaml 
```cd ~/my_gitlab/``` создать ```nano docker-compose.yaml``` в репозитории уже готовый, настроенный файл, скопировать оттуда.
3. Запуск ```docker compose up -d``` Остановка ```docker compose down```
4. Настроить сертификат для работы по https (только при необходимости)