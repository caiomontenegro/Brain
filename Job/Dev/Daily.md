
# Personal




docker exec -it mysql-8.0.32 mysql -u root -p12345678 strapi
INSERT INTO admin_users_roles_links (user_id, role_id) SELECT u.id, r.id FROM admin_users u, admin_roles r WHERE u.email = 'caio.montenegro@sejaefi.com.br' AND r.code = 'strapi-super-admin';

# A Fazer:

Colher Evidencias das FAQs em prod
Planjear API PIX

Pagespeed da página Bolix
- Fotos do hero
- swiper
- Tag manager precisa esperar pra rodar

simular um deploy para testar pagespeed.
run preview no final dockerfile
make run command="npm run build:testing"

glpat-ypH_1Aquv1L8slyPnZE7Om86MQp1OmI2CA.01.0y053moyc

# Daily:

Deploy no portal-frontend da última fase da atividade de FAQ's
Notifiquei o Diego, e me deixei a disposição para qualquer dúvida dele a respeito do novo fluxo

Montei um planejamento do Rework da página de API Pix do Portal
E iniciei atuação nela.


# Script de planejamento:

📋 Nome da tarefa
[data de início prevista]
Objetivo: uma linha descrevendo o que será feito e por quê
⏱ Estimativa total: X dias úteis — entrega em DD/MM
Etapas:
1. etapa — estimativa, ex: 4h
2. etapa — estimativa
3. etapa — estimativa
🔗 Dependências:
• o que precisa estar pronto antes — ex: acesso ao ambiente, definição de um requisito, outro time liberar algo
• (nenhuma, se for o caso)
⚠️ Riscos:
• risco → mitigação: o que você fará se acontecer
• (nenhum identificado, se for o caso)
🙋 Suporte esperado da liderança:
• ex: validação do critério de aceite antes de começar, ou "nenhum por enquanto"





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

