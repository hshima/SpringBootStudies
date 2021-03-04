# Spring boot

1. Problemas resolvidos pelo Spring Boot
2. Auto onfiguration
3. FatJar ou UberJar

___
## Problemas resolvidos pelo Spring Boot
### Antes da criação do Spring Boot, era necessário:
- Configurações de Beans em arquivos .xml
- Dispatcher Servlet e view resolver em web.xml
- Set up manual de Banco e dados
- Tempo gasto em configurações
- Perda de foco sobre o valor

### Vantagens
- Facilita set up de projetos Spring
- Não é necessário criar arquivos de configuração
- Foco na produtividade

#### Anatomia
Todas as dependências Spring Boot já se encontram em uma camada de abstração que invoca as dependências do Spring Framework, seguindo o seguinte esquema
```text
+ Spring Projects
+---+ Spring Boot
|   +--- Spring Web Services
|   +--- Spring Session
|   +--- Spring Kafka
|   +--- Spring Data
|   +--- Spring ...
+ Spring Framework
+--- Web
+--- Data
+--- AOP
+--- Core

```

### Produtividade - Set Up simplificado do projeto
Permite utilizar a criação inicial pelo portal [Start](https://start.spring.io/)ou na própria IDE.

#### Exemplo de dependência
```text
+ spring-boot-starter-web
|
+---+ spring-boot-starter
|   +--- spring-boot
|   +--- spring-boot-autoconfigure
|   +--- spring-boot-starter-logging
|
+--- spring-web
|
+--- spring-webmvc
|
+---+ spring-boot-starter-tomcat
    +--- tomcat-embed-core
    +--- tomcat-embed-logging-juli
```

### Simplificação da execução
Não há necessidade de deploy em um servidor externo

### Configurações - arquivo externo para configuração
Existe um único arquivo externo (localização: `resources/application.properties`), simplificando a dependência para 

## Auto configuration

Anteriormente, para se trabalhar com web (mvc), era necessário configurar os arquivos spring-servlet e web.xml (DispatcherServlet - padrão front controller que realiza o redirecionamento aos controllers e páginas do Spring MVC).

Para outros tipos de desenvolvimento, era necessário manipular outros arquivos para ativar os beans.

A dependência responsável por realizar o `autoconfigure` se encontra no seguinte esquema

```text
+ spring-boot-starter-web
+---+ spring-boot-starter
    +--- spring-boot-autoconfigure
```

### Mecânica
Ao adicionar a dependência, o Spring validará a existência das anotações `@Configuration` e `@ConditionalOnClass`, que encontrará na Classe `org.springframework.boot.autoconfigure.web.servlet.WebMvcAutoConfiguration`.
Nessa auto configuração, são envolvidas as classes: 
- `Servlet.class`
- `DispatcherServlet.class`
- `WebMvcConfigurer.class`

## FatJar/UberJar
### Antes do Spring Boot
Passos necessários:
`
construir a aplicação -> empacotamento (.jar ou .war) -> deploy em servidor de aplicação (web container ou servidor de aplicações)
`
Além da necessidade do artefato web, era necessário manter todo o ambiente da aplicação atualizado.

### Empacotamento
Artefato pronto para execução. Nesse caso, embarca o servidor de aplicação às dependências do projeto:
```text
+ Fat/Uber
+---+ thin // App Dependencies
|   +--- skinny // App
+--- hollow // AppRuntime
```

### Rodar
```bash
mvn package && java -jar target/spring-boot-name-0.1.0.jar 
```
para rodar em um `.war`:
Alterar a configuração de dependência para:
```text
 - Maven: 
    <packaging>war</packaging>
    
 - Gradle: 
    apply plugin: 'war'
    war {
        basename = 'myapp'
        version = '0.5.0'
    }
```