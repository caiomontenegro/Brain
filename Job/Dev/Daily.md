
# Personal

matrícula: m16180824
Agência: 0001 Conta 593195-9
user ID Amplitude: 1069273043502

Recuperação Jira: GC0GA09PC4X4BZIHLI1F8P24


docker exec -it mysql-8.0.32 mysql -u root -p12345678 strapi
INSERT INTO admin_users_roles_links (user_id, role_id) SELECT u.id, r.id FROM admin_users u, admin_roles r WHERE u.email = 'caio.montenegro@sejaefi.com.br' AND r.code = 'strapi-super-admin';

# A Fazer:

- Abrir GMUDS - Feito
- Deploy Pagespeed - Feito
- Roda nova pipeline para subir redirects de mkt novo - Feito
- Subir novos documentos e contratos - Feito
- Validar tarefa da Amanda- Feito
- Confirmar se a tabela redirects funciona com o novo plugin sem necessidade de migração de dados - Feito
    - Se necessário fazer endpoint de migração da tabela
- ⁠Confirmar node 22 com strapi4 (ambiente local)
- Olhar com infra cloud configuração do ambiente de testes com node 22

# Daily:

**Tabela** 

**`redirects`**

 **— migração Strapi 4 → 5**

O Strapi 5, ao iniciar, adicionou 3 colunas novas à tabela existente:

**document_id** - obrigatória para o Strapi 5 reconhecer os registros
**locale** - não precisa de ação
**published_at** (datetime) — depende do draftAndPublish


No deploy, a infra precisa rodar:

```sql
UPDATE redirects SET document_id = UUID() WHERE document_id IS NULL;
```

se na collection draftAndPublish: true, também:

```sql
UPDATE redirects SET published_at = NOW() WHERE published_at IS NULL;
```


No caso atual, draftAndPublish: false, então só o primeiro comando é necessário.




 


## MR Projetos:

Conta digital - MR CD  
Backend Conta - MR BFF  
Template Builder - MR TBS  
Portal Frontend - MR portal frontend
Portal Backend - MR portal backend

## Vacation:

Julho


Folga 28
Trabalha 31.


