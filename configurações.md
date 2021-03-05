# Configurações com .yaml
Além dos arquivos de extensão .properties, é possível usar os arquivos de extensão .yaml, que tem sintaxe: chave: valor, e indentação similar ao Python.
```properties
basic.key.value = value
basic.key.message = value2
basic.key2.number = value3
```
```yaml
basic:
    key:
        value: value
        message: value2
    key2:
        number: value3
```

### Procedimento
Por padrão, a própria linguagem é capaz de realizar essa substituição, bastando realizar a atualização de extensão e arquivo.
1. Substituir os arquivos atuais do projeto para `.yml` ou `.yaml`
2. Compilar o projeto

## Hierarquia de configurações
1. Configurações embarcadas do servidor
2. Argumentos de linha de comando (CLI)
3. Arquivo de propriedades
4. configuração da anotação `@SpringBootApplication`

### Utilizando CLI

```bash
mvn spring-boot:run -Dserver.port=8085
```

Rodando a partir da pasta target, utilizando o package gerado em `mvn packge`, na porta `8085`
```bash
java -jar -Dserver.port=8085  springBootBootCamp-0.0.1-SNAPSHOT.jar
```
ou
```bash
java -jar springBootBootCamp-0.0.1-SNAPSHOT.jar --server.port=8085
```