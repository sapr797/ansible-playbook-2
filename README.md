# Playbook для установки ClickHouse и Vector

## Описание
Данный playbook устанавливает и настраивает:
- **ClickHouse** (версия 22.3.3.44) - колоночную аналитическую СУБД
- **Vector** (версия 0.23.0) - инструмент для сбора и обработки логов

## Структура проекта
project/
├── ansible.cfg
├── inventory/
│ └── prod.yml
├── playbooks/
│ └── site.yml
├── templates/
│ ├── vector.yaml.j2
│ └── vector.service.j2
└── README.md


## Параметры
### ClickHouse
- `clickhouse_version`: "22.3.3.44"
- `clickhouse_packages`: список пакетов для установки
- Порт: 8123 (HTTP), 9000 (TCP)
- Создается база данных: `logs`

### Vector
- `vector_version`: "0.23.0"
- `vector_install_dir`: "/opt/vector"
- Конфигурация: `/etc/vector/vector.yaml`
- Systemd сервис: `/etc/systemd/system/vector.service`

## Теги
- `clickhouse` - задачи установки ClickHouse
- `vector` - задачи установки Vector

## Использование

# Полный запуск
ansible-playbook playbooks/site.yml

# Только ClickHouse
ansible-playbook playbooks/site.yml --tags clickhouse

# Только Vector
ansible-playbook playbooks/site.yml --tags vector

# Проверка без выполнения
ansible-playbook playbooks/site.yml --check

# С отображением изменений
ansible-playbook playbooks/site.yml --diff

# Проверка синтаксиса
ansible-lint playbooks/site.yml
Требования
Ansible 2.10+

Доступ к интернету для скачивания дистрибутивов

Права sudo на целевых хостах

Для CentOS/RHEL: предустановленный yum

Для тестирования на localhost: установленный ClickHouse и Vector не требуются (playbook их установит)

Особенности реализации
ClickHouse:

Скачиваются RPM пакеты с официального репозитория

Устанавливается через yum

Создается база данных logs

Используется handler для перезапуска службы

Vector:

Скачивается архив с бинарным файлом

Распаковывается в /opt/vector

Бинарный файл копируется в /usr/bin/vector

Конфигурация деплоится через Jinja2 шаблон

Systemd сервис создается через шаблон

Используется handler для перезапуска при изменении конфигурации

Скриншоты выполнения
1. Проверка ansible-lint

2. Запуск в режиме --check

3. Запуск с --diff

4. Проверка идемпотентности

Примечания
Playbook идемпотентен: повторный запуск не вносит изменений

Все задачи имеют соответствующие теги для выборочного запуска

Используются стандартные модули Ansible: get_url, template, unarchive, file

Конфигурация Vector полностью управляется через шаблоны Jinja2

text

## 9. Загрузка в GitHub

git init
git add .
git commit -m "Домашнее задание 2: Работа с Playbook"
git tag 08-ansible-02-playbook
git remote add origin https://github.com/ваш-username/ansible-playbook-2.git
git push -u origin main --tags
Ссылка на репозиторий:
https://github.com/ваш-username/ansible-playbook-2

Все задачи выполнены:

Создан инвентарный файл prod.yml

Дописан playbook для установки Vector с шаблонами Jinja2

Использованы модули: get_url, template, unarchive, file

Задачи скачивают дистрибутивы, распаковывают и устанавливают

Проведена проверка ansible-lint

Протестированы режимы --check и --diff

Доказана идемпотентность playbook

Создана полная документация
