# Mudi

**Aplicação desenvolvida utilizando:**

- Spring Framework
  - Spring Data
  - Spring MVC 
  - Spring Security
- Bootstrap
- thymeleaf
- Vue.js

**Foco no aprendizado do Spring MVC e Security. O front é apenas para visualizar o funcionamento.**

# Funcionamento

Codigo para criação das tabelas do Spring Security (**Necessario antes de iniciar a aplicação**)

```sql
create table users(
    username varchar_ignorecase(50) not null primary key,
    password varchar_ignorecase(500) not null,
    enabled boolean not null
);

create table authorities (
    username varchar_ignorecase(50) not null,
    authority varchar_ignorecase(50) not null,
    constraint fk_authorities_users foreign key(username) references users(username)
);
create unique index ix_auth_username on authorities (username,authority);
```

**Criação de um usuario em codigo**

Dentro da classe "**WebSecurityConfig**" modifique o metodo **configure** para: 
```java
 @Override
protected void configure(AuthenticationManagerBuilder auth) throws Exception {
        BCryptPasswordEncoder encoder = new BCryptPasswordEncoder();

        UserDetails user =
        User.builder()
        .username("Nome do Usuario")
        .password(encoder.encode("Senha"))
        .roles("ADM")
        .build();

        auth.jdbcAuthentication()
        .dataSource(dataSource)
        .passwordEncoder(encoder)
        .withUser(user);
```

**Pagina inicial**

>**/home**

Qualquer outro vai acessar a pagina de login.

**API REST**

Json com todos os pedidos aguardando:
> **/api/pedidos/aguardando**

Json do interceptador com as informações de performance da aplicação
>**/acessos**


### Banco de dados: MySQL
