
# sonar-ldap-docker

Executar:

    git clone https://github.com/Lhuckaz/sonar-ldap-docker.git
    cd sonar-ldap-docker

Trocar em docker-compose.yml o PGHOST para o IP do seu host

    environment:
        - SONARQUBE_JDBC_USERNAME=sonar
        - SONARQUBE_JDBC_PASSWORD=sonar
        - SONARQUBE_JDBC_URL=jdbc:mysql://192.168.0.10
        
Configurar LDAP em sonar_conf/sonar.properties conforme sua configuração

    sonar.security.realm=LDAP
    sonar.security.savePassword=true
    ldap.url=ldap://dc01.empresa.corp:389
    ldap.bindDn=CN=USR,OU=Contas,OU=InfraEstrutura,DC=empresa,DC=corp
    ldap.bindPassword=senha
    ldap.authentication=simple
    ldap.user.baseDn=DC=empresa,DC=corp
    ldap.group.baseDn=DC=empresa,DC=corp
    ldap.user.realNameAttribute=displayName
    ldap.user.emailAttribute=mail
    ldap.group.idAttribute=sAMAccountName
    ldap.user.request=(&(objectClass=user)(sAMAccountName={login}))

        
Trocar em sonar_conf/sonar.properties o sonar.jdbc.url para o IP do seu host

    sonar.jdbc.url=jdbc:mysql://192.168.0.10:3306/sonar?useUnicode=true&characterEncoding=utf8&rewriteBatchedStatements=true&useConfigs=maxPerformance
    
Ao final das configurações, executar:

    docker-compose up

Acessar http://\<host\>:9000 <br />
Usuario: admin <br />
Senha: admin

**Obs.:** Para nao utilizar LDAP apagar todas as configuraçoes do LDAP e o plugin da pasta ``/sonar_plugins``
