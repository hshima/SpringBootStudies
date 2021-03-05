# Profiles e Configurações
1. Importância do uso de Profiles
2. Configurações com arquivos .properties
3. Configurações com arquivos .yaml
4. Configurações com comand line - CLI
5. Configurações de variáveis de ambiente - interpretação como linhas de configurações no arquivo

___

## Profiles
### Porque manter múltiplos ambientes
- Isolar os bancos de dados para cada ambiente
- Execução de testes unitários em ambiente local
- Suíte de testes completas em ambiente de teste
- Similação do ambiente real em staging
- deploy simplificado em produção

### Como o Spring Boot funciona
- Configurações próprias para cada ambiente
- Ambientes com sua configuração: dev, production

## Configurações com properties
1. No projeto, criar os arquivos dos respectivos ambientes
```properties
# application-prod.properties
app.message=This is the property file for {spring.application.name}
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
spring.datasource.url=<MYSQL_URL>
spring.datasource.username=<USERNAME>
spring.datasource.password=<PASSWORD>
```
```properties
# application-dev.properties
app.message=This is the property file for {spring.application.name}
spring.datasource.driver-class-name=org.h2.Driver
spring.datasource.url=jdbc:h2:mem:db;DB_CLOSE_DELAY=-1
spring.datasource.username=sa
spring.datasource.password=sa
```
2. Criar o arquivo para mapear as configurações:
```java
// src/main/java
// com.gft.springBootConfig.config.DBConfiguration

@Configuration // Bean que declara ao Spring que se trata de uma configuração
@ConfigurationProperties

```

