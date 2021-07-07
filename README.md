# keycloak-cluster-setup
Конфигурация кластера keycloak для чотких пацанов

//TODO

1. Скачать данный репозиторий
2. Перейти в директорию кейклока
3. bin/jboss-cli.sh --file=./cli-scripts/configure-hostname.cli
4. bin/jboss-cli.sh --file=./cli-scripts/configure-https.cli
5. bin/jboss-cli.sh --file=./cli-scripts/configure-database.cli
6. bin/jboss-cli.sh --file=./cli-scripts/configure-caches.cli
7. sudo cp cli-scripts/haproxy.cfg /etc/haproxy/haproxy.cfg
8. sudo cp cli-scripts/haproxy.crt.pem /etc/haproxy
9. bin/jboss-cli.sh --file=./cli-scripts/configure-proxy.cli
10. bin/jboss-cli.sh --file=./cli-scripts/configure-session-affinity.cli
11. bin/standalone.sh -c standalone-ha.xml -Djboss.node.name=kc1
12. bin/standalone.sh -Djboss.socket.binding.port-offset=100 -c standalone-ha.xml -Djboss.node.name=kc2
13. bin/standalone.sh -Djboss.socket.binding.port-offset=200 -c standalone-ha.xml -Djboss.node.name=kc3
