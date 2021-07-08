# keycloak-cluster-setup
Конфигурация кластера keycloak для чотких пацанов

## Необходимые требования 
- Git
- Java 8
- HAProxy
- Postgres (На самом деле можно любую базу подрубить, но в данном проекте лежит драйвер для postgres)

## Порядок действий
0. Поставить звездочку проекту
   

1. Прописать в etc/hosts localhost mykeycloak (На самом деле можно прописать любой урл и сконфигурировать под него, но в данном проекте используется урл фронта, keystore и сертификат для https://mykeycloak)


2. Скачать данный репозиторий


3. Перейти в директорию кейклока


4. Сконфигурировать host в standalone-ha.xml: 
   
`bash bin/jboss-cli.sh --file=./cli-scripts/configure-hostname.cli`
5. Сконфигурировать https в standalone-ha.xml:

`bash bin/jboss-cli.sh --file=./cli-scripts/configure-https.cli`

6. В файле /cli-scripts/configure-database.cli прописать конфиг соединения к БД, которую будет использовать keycloak


7. Сконфигурировать  подключение к БД в standalone-ha.xml: 
   
`bash bin/jboss-cli.sh --file=./cli-scripts/configure-database.cli`

8. Сконфигурировать кэши в standalone-ha.xml: 
   
`bash bin/jboss-cli.sh --file=./cli-scripts/configure-caches.cli`

9. Сконфигурировать HAProxy:

`sudo cp cli-scripts/haproxy.cfg /etc/haproxy/haproxy.cfg`

10. Сконфигурировать сертификат для HAProxy: 
    
`sudo cp cli-scripts/haproxy.crt.pem /etc/haproxy`

11. Сконфигурировать прокси в standalone-ha.xml: 
    
`bin/jboss-cli.sh --file=./cli-scripts/configure-proxy.cli`
12. Сконфигурировать привязку сессий в standalone-ha.xml: 
    
`bin/jboss-cli.sh --file=./cli-scripts/configure-session-affinity.cli`

13. Запустить ноду KC1 в режиме кластера: 
    
`bin/standalone.sh -c standalone-ha.xml -Djboss.node.name=kc1`
14. Запустить ноду KC2 в режиме кластера: 
    
`bin/standalone.sh -Djboss.socket.binding.port-offset=100 -c standalone-ha.xml -Djboss.node.name=kc2`

15. Запустить ноду KC3 в режиме кластера: 
    
`bin/standalone.sh -Djboss.socket.binding.port-offset=200 -c standalone-ha.xml -Djboss.node.name=kc3`
