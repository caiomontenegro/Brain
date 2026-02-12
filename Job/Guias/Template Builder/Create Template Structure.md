
## Setting up the route

First we to create the routes. 

Access the folder:

`server/api`

Create a new directory and name it after the service. Example: 

`multiple-card`

Within it, create the two more new folders:

`email`
`pdf`

Within email, create one more folder and name it after e-mail/template you are creating. Example:

`auto-debit`

Within this new folder, create a new TS file named:

`index.post.ts`

The structure will be:

![[Brain/Job/Guias/Template Builder/assets/diretorio.png]]

Copy all content of another index.post.ts, but change only redirect routes block code:

```
import useS3 from '@/composables/useS3.js';
import useUtils from '@/composables/useUtils.js';

export default defineEventHandler(async (event: any) => {
  const config = useRuntimeConfig();
  const body = await readBody(event);
  const s3Config = {
    NUXT_URL: config.NUXT_URL,
    S3_BUCKET: config.S3_BUCKET,
    S3_REGION: config.S3_REGION,
    S3_PATH: config.S3_PATH,
    S3_ENDPOINT: config.S3_ENDPOINT,

  };

  const { uploadToS3, deleteFromS3 } = useS3();
  const { sanitizeHtml } = useUtils();

  try {
    const filename = `${crypto.randomUUID()}.json`;
    await uploadToS3(body, filename, s3Config);

    // @ts-ignore

    let emailContent = (await $fetch(`${config.NUXT_URL}/<sua rota>`, {
      query: { filename, mock: body.mock },
    })) as string;

    emailContent = sanitizeHtml(emailContent);
    const resS3 = await deleteFromS3(filename, s3Config);

    if (resS3?.error) {
      event.node.req.logger.error(resS3.message, {
        error: resS3.error || 'Mensagem não encontrada'
      });
    }
    return { emailContent };
    
  } catch (error: any) {
    throw new Error(error);
  }
});
```

exemple:

```
let emailContent = (await $fetch(`${config.NUXT_URL}/multiple-card/email/auto-debit`, {
      query: { filename, mock: body.mock },
    })) as string;

const body = {
      message: 'Erro na requisição: multiple-card/email/auto-debit',
      error: error.message,
    };
```



## Create Template


Access the Pages directory, and recreate the folder structure that we create previously. Example:


![[diretorio2.png]]


O arquivo index.vue será o template do e-mail. Para iniciar com uma configuração padrão. Utilize esse conteúdo:

<template>
  <mail-container>
    <mail-header :color="headerColor" />
    <mail-row>

      
    </mail-row>

    <mail-contact-footer />
  </mail-container>
</template>

```
<script setup>
import MailRow from '@/components/email/MailRow.vue';
import MailIcon from '@/components/email/MailIcon.vue';
import MailCard from '@/components/email/MailCard.vue';
import MailContactFooter from '@/components/email/MailContactFooter.vue';
import MailHeader from '@/components/email/MailHeader.vue';
import MailContainer from '@/components/email/MailContainer.vue';
// criar
import geolocationCodeMock from '~/mocks/account/email/geolocationCodeMock.js';


const route = useRoute();
let emailData = '';

if (route.query.mock) {
  emailData = geolocationCodeMock;
  emailData.modality = route.query.modality ?? geolocationCodeMock.modality;
} else {
  const config = useRuntimeConfig();
  if (process.server) {
    const s3Config = {
      NUXT_URL: config.NUXT_URL,
      S3_BUCKET: config.S3_BUCKET,
      S3_REGION: config.S3_REGION,
      S3_PATH: config.S3_PATH,
      S3_ENDPOINT: config.S3_ENDPOINT,
    };
    const useS3Composable = await import('@/composables/useS3.js');
    const useS3 = useS3Composable.default || useS3Composable;
    const { readFromS3 } = useS3();
    emailData = await readFromS3(route.query.filename, s3Config);
  }
}

const { logoUrl, btnColor, color, headerColor } = useTemplateCustom(emailData);
</script>
```


## Adding images

To add new dinamic images on template, we need to request to infra-cloud.

Check the note to [[Adding Dinamic Images]] and follow the guide.


Após documentar o contrato que deseja receber, mande esse contrato para o seu backend. Para que ele possa preparar a rota e retornar os dados através da mesma.


## Template

For test the visual tempalte, run the commando:

```
make up dev-preview
```

No browser, acesse a rota:

https://template-builder-service.m16180824.orp-1.colaboradores.labgerencianet.com.br/<rota-para-page>?mock=true

exemplo:

https://template-builder-service.m16180824.orp-1.colaboradores.labgerencianet.com.br/insurance/email/trusted-contact?mock=true


SWAGGER

1 - Configuração

Acesse o diretório "docs", e depois no arquivo "template-builder.yaml". Configure esse padrão de sessão e rotas:

 # ======= Rotas - <Nome da Sessão> =======
  /api/<fluxo>/email/<produto do fluxo>/<parte específica do produto>:
    $ref: "./<rota do arquivo da conterá as informações da rota>"

Exemplo:

 # ======= Rotas - Seguros =======
  /api/insurances/email/invoice-paid/trusted-contact:
    $ref: "./insurances/email/invoice-paid/trusted-contact/trusted-contact.yaml"

2 - Criando o swagger

Ainda dentro do diretório "docs", crie um novo diretório com o nome do fluxo, por exemplo "Seguros". Dentro desse diretório crie novamente a estrutura de diretórios de "email" e se necessário também de "pdf. Ex:

docs > insurance > email
                 > pdf

Dentro de email, criaremos dois novos arquivos de yaml, o primeiro deles será com o nome do nosso email. Exemplo: trusted-contact.yaml

Dentro desse arquivo iremos adicionar esse padrão de configuração:

post:
  tags:
    - Seguros // Nome da Sessão
  summary: "E-mail enviado para contato de confiança ao contratar seguro fatura paga" // Descrição do email

  parameters:
    - in: "header"
      name: "Authorization"
      required: true
      description: "Token Bearer"
      schema:
        type: "string"

  requestBody:
    required: true
    content:
      $ref: ./request-body.yaml // rota para o arquivo que dará instruções do schema.

  responses:
    200:
      description: "Success"
      content:
        application/json:
          schema:
            type: object
            properties:
              emailContent:
                type: string
                description: Conteúdo HTML do email
                example: "<!DOCTYPE html><html><head>...</head><body>...</body></html>"
            required:
              - emailContent
    401:
      description: "Unauthorized"
    500:
      description: |
        Internal Server Error


E um outro arquivo que dará instruções para o schema. Exemplo:
request-body.yaml

E dentro desse arquivo usaremos esse padrão:

application/json:
  schema:
    type: object
    properties:
      modality:
        type: string
        summary: Modalidade da conta
        example: "pro"
      coverages:
        type: "object"
        required:
          - identifier
        properties:
          identifier:
            type: string
            summary: Cobertura do seguro
            example: morte
          deductible:
            type: object
            required:
              - value
              - unit
            properties:
              value:
                type: "number"
                summary: "Valor da unidade da franquia"
                example: 1
              unit:
                type: "string"
                summary: "Unidade da franquia"
                example: "days"
          value:
            type: "number"
            summary: "Valor das parcelas de quitação de saldo"
            example: 500000
    required:
      - modality
      - insured
      - coverages

Para visualizar o swagger. Basta baixar a extensão do VSCode "Swagger Viewer". Depois
clique com o botão direito no arquivo template-builder.yaml dentro do diretório "docs"
clique em "Preview Swagger".
