# keycloak-cluster-setup
Конфигурация кластера keycloak для чотких пацанов

## Необходимые требования 
- Java 8
- HAProxy
- Postgres (На самом деле можно любую базу подрубить, но в данном проекте лежит драйвер для postgres)

## Порядок действий
0. Поставить звездочку проекту
1. Прописать в etc/hosts localhost mykeycloak (На самом деле можно прописать любой урл и сконфигурировать под него, но в данном проекте используется урл фронта, keystore и сертификат для https://mykeycloak)
2. Скачать данный репозиторий
3. Перейти в директорию кейклока
4. bin/jboss-cli.sh --file=./cli-scripts/configure-hostname.cli
5. bin/jboss-cli.sh --file=./cli-scripts/configure-https.cli
6. В файле /cli-scripts/configure-database.cli прописать конфиг соединения к БД, которую будет использовать keycloak
7. bin/jboss-cli.sh --file=./cli-scripts/configure-database.cli
8. bin/jboss-cli.sh --file=./cli-scripts/configure-caches.cli
9. sudo cp cli-scripts/haproxy.cfg /etc/haproxy/haproxy.cfg
10. sudo cp cli-scripts/haproxy.crt.pem /etc/haproxy
11. bin/jboss-cli.sh --file=./cli-scripts/configure-proxy.cli
12. bin/jboss-cli.sh --file=./cli-scripts/configure-session-affinity.cli
13. bin/standalone.sh -c standalone-ha.xml -Djboss.node.name=kc1
14. bin/standalone.sh -Djboss.socket.binding.port-offset=100 -c standalone-ha.xml -Djboss.node.name=kc2
15. bin/standalone.sh -Djboss.socket.binding.port-offset=200 -c standalone-ha.xml -Djboss.node.name=kc3
