
# Personal

matrícula: m16180824
Agência: 0001 Conta 593195-9
user ID Amplitude: 1069273043502

Recuperação Jira: GC0GA09PC4X4BZIHLI1F8P24


docker exec -it mysql-8.0.32 mysql -u root -p12345678 strapi
INSERT INTO admin_users_roles_links (user_id, role_id) SELECT u.id, r.id FROM admin_users u, admin_roles r WHERE u.email = 'caio.montenegro@sejaefi.com.br' AND r.code = 'strapi-super-admin';

# A Fazer:

- Google Tag Manager
  - Download LAB
- Code review Amanda
- Fazer cursos Hacker Rangers
- Encerrar Gmuds


Pagespeed da página Bolix
- Fotos do hero
- swiper
- Tag manager precisa esperar pra rodar


run preview no final dockerfile
make run command="npm run build:testing"



# Daily:

Colher evidencia de:
texto de definição
link de boletos


patch/atualiza-node patch/atualiza-versao-strapi patch/content-types-redirect patch/remocao-gulp



# CAB

- Mudanças no BFF do conta Digital
- E no Aplicativo do Conta Digital

Uma nova funcionalidade que Contempla ambos os projetos:
- Solicitação de aumento de limite por parte do cliente
  Será feito através do menu de limites, onde clientes habilitados poderão visualizar um botão de solicitação.
  Será direcionado um formulário: Com valor atual e um campo do limite desejado.
  Intervalo mínimo entre solicitações de 90 dias
  Registro  da data de solicitação. Com registros:
  Cliente, data/hora, limite atual, limite desejado, status inicial (Em análise)
  Bloqueio visual e funcional.

Demais tarefas, todas no conta digital:
- Atualização nos valores das tarifas de anuidade de cartão
- Envio dos documentos CPF ou CNPJ em TED comum e programado, para uma validação antes do envio da transferência.
- Correção de busca de cliente no menu de emissão de cobranças, onde o sistema não estava localizando de maneira correta nomes completos.




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

Backend Conta Digital - MR BFF
App Conta Digital - MR CD
Design System - MR DS
Login Provider - MR LP
Pay frontend - MR PAY
Download Lab - MR download
Template builder Service - MR TBS
Design System Nuxt - MR ds-nuxt
GN Registration - MR gn-registration-ui
MS Marketing - MR ms-marketing
Pix Frontend - MR pix-frontend
PIX UI - MR pix-ui
Portal Backend - MR portal-backend
Protal Frontend - MR portal-frontend
Portal Lab - MR portal-lab

## Vacation:

