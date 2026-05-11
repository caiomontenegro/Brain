
# Personal

matrícula: m16180824
Agência: 0001 Conta 593195-9
user ID Amplitude: 1069273043502

Recuperação Jira:GC0GA09PC4X4BZIHLI1F8P24



# A Fazer:
Criar pasta docs
documentando como rodar o projeto do portal backend


# Daily:

- Captura e Persistencia de Parametros URL no Portal Frontend
  Arthur validou o code da tarefa. 
  Fizemos deploy
  Eu acabei encontrando um bug enquanto coletava evidências em prod. em caso de acesso sem parametros, acionamos um fallback que identifica as chaves ['none', 'direct', '(none)', '(direct)'] no acquisition_campaign do local storage, para enviar um UTM de "Portal". Porém agora ocorreu uma nova chave: '(not set)' que não havia acontecido, por esse motivo ele não caiu no fallback.
  Ajustei e criei um MR e vamos subir essa correção na primeira oportunidade
- Tarefa de Vulnerabilidades do Portal Backend.
  Eu fiz uma atualização de todos os plugins que não são compatíveis com o Strapi 5
  Porém, um único plugin não é compatível com o Strapi 5 e já foi descontinuado. A função dele é que ele permite cadastrar redirects de URL (ex: /pagina-antiga → pagina nova) pelo admin do Strapi. O frontend consultava essa lista para redirecionar o usuário.
  
**Duas opções:**

1. **Simples** — Criar um content-type "Redirect" direto no Strapi com campos source, destination e statusCode. Sem dependência externa, mas interface básica.
    
2. **Robusta** — Instalar o 
    strapi-plugin-redirect-manager
     (compatível com Strapi 5). É só adicionar no package.json e rodar npm install. Tem interface dedicada, mas é plugin de terceiro relativamente novo.

Conversei com o diego, e ele me passou que O plugin é usado para redirecionar páginas descontinuadas (ex: posts de blog removidos) e foi muito utilizado na época da migração de domínio. Hoje o uso é bem menor e não há uma pessoa específica responsável por ele. Além disso, cada novo redirect exige rebuild do projeto por causa do sistema de rotas do Nuxt. Diego mencionou que faz tempo que não usam com frequência.

 Por isso eu acho que a melhor alternativa é substituir o plugin  por um content-type nativo no Strapi com campos source, destination e statusCode. O time continua gerenciando redirects pelo painel admin. No frontend, vamos consumir esses dados via middleware em runtime, eliminando a necessidade de rebuild a cada novo redirect. Os poucos redirects ativos serão recadastrados manualmente.
 
 



## MR Projetos:

Conta digital - MR CD  
Backend Conta - MR BFF  
Template Builder - MR TBS  
Portal Frontend - MR Portal frontend
Portal Backend - MR Portal backend

## Vacation:

Maio 2

Folga 8
Férias 11 a 20
Day off 21
Folga 22
Folga 25
Trabalha 29


Julho

Folga 10
Férias 13 a 27
Folga 28
Trabalha 31.


