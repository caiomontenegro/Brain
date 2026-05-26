Resolução de vulnerabilidades no backend


Etapas

## Atualizar Strapi

### Arquivos modificados:
##### package.son !!!!!
  
  Dependências removidas (temporariamente)
  - ```plaintext
    @_sh/strapi-plugin-ckeditor
     (~3.0.9) — incompatível com Strapi 5, será migrado depois
    
    strapi-plugin-multi-select
     (~1.2.3) — incompatível com Strapi 5

    strapi-plugin-redirects
     (~1.0.4) — incompatível com Strapi 5

    @strapi/plugin-seo
     (~1.9.9) — precisa da versão 2.x para Strapi 5, será migrado depois
    ```
    
    Dependências atualizadas:

| Pacote                                                  | Antes (v4) | Depois (v5) |
| ------------------------------------------------------- | ---------- | ----------- |
| ```plaintext<br>@strapi/strapi<br>```                   | ~4.25.23   | ~5.42.0     |
| ```plaintext<br>@strapi/plugin-i18n<br>```              | ~4.25.23   | ~5.42.0     |
| ```plaintext<br>@strapi/plugin-users-permissions<br>``` | ~4.25.23   | ~5.42.0     |
| ```plaintext<br>@strapi/provider-upload-aws-s3<br>```   | ~4.25.23   | ~5.42.0     |
| ```plaintext<br>react-router-dom<br>```                 | ~5.3.4     | ~6.28.0     |
| ```plaintext<br>styled-components<br>```                | ~5.3.3     | ~6.1.0      |

O  react-router-dom e styled-components foram atualizados porque o admin do Strapi 5 exige essas versões maiores.

Adições:

``` "type": "commonjs"```

Declaração explícita do sistema de módulos, já que o Strapi 5 suporta ESM e CJS, e o projeto usa require()



Atualizar Node infra
Analise do sudo do GulpFile.



 
##### app.js
Atualizado, para ser uma nova API de inicialização do Strapi 5

##### index.js
Atualizando src/index.js para Strapi 5 — a API de register/bootstrap é compatível, mas strapi.db.connection muda.

##### config/admin.js
Atualizando config/admin.js para Strapi 5 — adicionando transfer.token.salt que é obrigatório no v5.
#####  Atualizar config/plugins.js 
Desabilitando plugins incompatíveis com Strapi 5 temporariamente, atualizando provider upload

##### healthcheck.js
Atualizando healthcheck controller — no Strapi 5, strapi.db.connection muda para strapi.db.getConnection().

##### Migration Custom Fields !!!!!
Com a remoção temporária de plugins incompátiveis, foi esse arquivo referência com os campos originais para restaurar após a migração dos plugins

##### Custom Fields !!!! 
Foram editaos por conta da remoção temporaria dos plugins.
##### Novo Diretório Config/Local 
Strapi 5 detecta conflito entre config.json e config.js, além disso o Strapi 5 muda a configuração do banco. O register() no src.index.js tenta configurar o banco, mas no Strapi 5 o banco é inicializado antes do register() ser chamado.

Portanto o config.json e databases.json foram movidos para essa pasta.

- config.js
  Teve as referências atualizadas.

##### Novo arquivo config/database.js
No Strapi 5 a configuração do database deve vir antes do register(), portanto esse arquivo foi criado para carregar as configurações que estavam contidas no index.js
