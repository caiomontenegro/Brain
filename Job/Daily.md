
# Personal

matrícula: m16180824
Agência: 0001 Conta 593195-9
user ID Amplitude: 1069273043502

Recuperação Jira:GC0GA09PC4X4BZIHLI1F8P24



# A Fazer:
Criar pasta docs
documentando como rodar o projeto do portal backend


# Daily:






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



## Tarefa de Captura e Persistência de Parâmetros


quando vier utm source, buscar o utm (Diego ainda vai definir)  salva-los em cookie. Tomar cuidado para não salvar isso no server side, deve ser salvo no CLIENT SIDE.

o que seta no local storage a gente vai sempre usar o actualVisit 

1- Identificar o middle que salva os cookies esta em session.global (registra todos os UTMS e Querys params na visita atual e primeira visita do cliente) em Actual Visit.

2- UseAppLinks o que trás no visitData(getmetadata) no utm??

3- jogar no useApplinks.ts e concatenar no link.

4- substituir o QRcode estatico por uma lib que gere o QR desses links e use-os

Dúvidas:
Existem locais que já não utilizavam os appLinks através da composables, 

Mapear os QR's e subir para bugbash

Links e QR's solicitação de cartão:
https://portal-frontend.m16180824.orp-1.colaboradores.labgerencianet.com.br/efi-bank/cartoes
https://portal-frontend.m16180824.orp-1.colaboradores.labgerencianet.com.br/efi-bank/cartao-de-credito-pf
https://portal-frontend.m16180824.orp-1.colaboradores.labgerencianet.com.br/efi-bank/cartao-de-credito-pj

Links e QR's abertura de conta:

(Após abrir aconta) 
https://portal-frontend.m16180824.orp-1.colaboradores.labgerencianet.com.br/abrir-conta 
(Botão "Abrir conta gratuita" e acessar o modal)
https://portal-frontend.m16180824.orp-1.colaboradores.labgerencianet.com.br/efi-bank/cartoes
https://portal-frontend.m16180824.orp-1.colaboradores.labgerencianet.com.br/efi-bank/cartao-de-credito-pf
https://portal-frontend.m16180824.orp-1.colaboradores.labgerencianet.com.br/efi-bank/cartao-de-credito-pj


Para abertura de contas:

```
<Qrcode
  class="h-[24rem] w-[24rem] max-h-[24.8rem]"
  ecc="M"
  :value="getOpenAccountCtaLink()"
/>

import { useAppLinks } from '@composables/useAppLinks';
const { getOpenAccountCtaLink } = useAppLinks();
```

Para solicitação de cartão de crédito

```
<Qrcode
  class="h-[24rem] w-[24rem] max-h-[24.8rem]"
  ecc="M"
  :value="getCardsCtaLink()"
/>

import { useAppLinks } from '@composables/useAppLinks';
const { getCardsCtaLink } = useAppLinks();
```