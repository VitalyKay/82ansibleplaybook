# ДЗ 8.2 Работа с Playbook

### Playbook [site.yaml](site.yml) устанавливает на managed host clickhouse и vector. Состоит из 2-х Play:
1. **Install Clickhouse** - включает 4 tasks, 1 handler, tags: *clickhouse*
  - **Get clickhouse distrib** - загрузка пакетов установки сервера и клиента clickhouse, tags: *download*
  - **Install clickhouse packages** - установка пакетов clickhouse, tags: *install*
  - **Flush handlers** - запуск хендлера Start clickhouse service, вызванного в предыдущей таске, для запуска сервера. Необходимо для выполнения следующей таски
  - **Create database** - создание БД logs на сервере clickhouse, tags: *create_db*
2. **Install Vector** - включает 3 tasks, в переменную окружения PATH добавляется путь к исполняемому файлу vector, tags: *vector*
  - **Get Vector distrib** - загрузка архива с Vector'ом, tags: *download*
  - **Create a vector directory if it does not exist** - создание директории vector в домашней директории, если она не существует, tags: *directory*
  - **Unzip Vector** - извлечение файлов Vector в директорию vector, tags: *unzip*

### Параметры, задаются в файле [vars.yml](group_vars/clickhouse/vars.yml)
1. **clickhouse_version** - версия пакетов clickhouse, по-умолчанию *22.3.3.44*
2. **clickhouse_packages** - имена пакетов, список
  - *clickhouse-client*
  - *clickhouse-server*
  - *clickhouse-common-static*
3. **vector_version** - версия вектора, по-умолчанию *0.22.2*