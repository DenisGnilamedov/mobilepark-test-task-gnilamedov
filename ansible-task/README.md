### Requirements:
* Ansible-galaxy collection install community.docker

**ТЗ выполняется двумя плейбуками. Запускать командами:**
* `ansible-playbook -vi inventory.ini --ask-become-pass configure-servers.yml` - Создает пользователей на воркерах (админ-1 на воркер-1 и т.д.), ставит докер на воркерах и мастере, ставит необходимый софт на воркерах
* `ansible-playbook -vi inventory.ini --ask-become-pass create_cluster.yml` - Инициализирует кластер (либо просто берет токен для воркеров) и добавляет воркеров в кластер.
