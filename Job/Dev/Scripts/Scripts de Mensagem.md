
## Scripts de Jira

#### Documentação do card:

##### Evidencias

Evidências  
Desenvolvimento
Testes Unitários 

##### Aprovação do Produto

Aprovação do Produto 

##### Plano de riscos

Plano de Riscos

Descrição: 
Probabilidade: Muito Baixa  
Impacto: Muito Baixo  
Descrição do Impacto: 

## Scripts para PM

### Aprovação:

Atuei na demanda <Título do card> e preciso de sua aprovação para encaminharmos para deploy assim que possível. Toda os detalhes da demanda bem como evidências do desenvolvimento estão nesse card EDS-<Número do card>. Assim que possível poderia nos formalizar sua aprovação? :slightly_smiling_face:

### Fim de Deploy

[@felipe.vasconcelos](https://gerencianet.slack.com/team/UTF9VQUA0) Deploy do CD realizado com sucesso, evidências coletadas e GMUDs finalizadas:  
[Documentação -Web Automations]()


| Rota                                           | Projeto                                                                                                                          |
| ---------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| ```plaintext<br>app.sejaefi.com.br<br>```      | ```plaintext<br>app-conta-digital<br>```                                                                                         |
| ```plaintext<br>login.sejaefi.com.br<br>```    | ```plaintext<br>auth<br>```                                                                                                      |
| ```plaintext<br>download.sejaefi.com.br<br>``` | ```plaintext<br>app-conta-digital<br>```<br><br> (referenciado via <br><br>```plaintext<br>VITE_APP_DOWNLOAD_URL<br>```<br><br>) |
| ```plaintext<br>pix.sejaefi.com.br<br>```      | ```plaintext<br>pix-ui<br>```<br><br> (confirmado pelo <br><br>```plaintext<br>VUE_APP_IMG_PATH<br>```<br><br>)                  |