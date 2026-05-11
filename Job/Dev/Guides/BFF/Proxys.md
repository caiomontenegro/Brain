Um proxy, que nada mais é que o "intermediário" entre o cliente (frontend) e o servidor (backend). O Proxy serve para:

- Redirecionar chamadas da API do front para serviços backend reais.
- Ocultar URLs reais dos serviços (deixa o front mais limpo).
- Adicionar headers ou tokens automaticamente.
- Resolver problemas de CORS (muito comum no dev).
- Cache, log ou auditoria no meio do caminho.
- Fazer transformações de dados, se necessário.
  
First, we need identify which category does the proxy belong to. Example:

The route proxy return the user balances. So the category be like a Balance. 

If we don't have any folder or other proxy with this caregory we need to create it. 

Para isso, vamos realizar alterações em 3 diretórios:

- server/config/routes>private
- server/app/controllers
- server/app/modules/business

Vamos criar arquivos JS de mesmo nome em cada diretório para criar um arquivo JS, para determinado produto/serviço de nova aplicação. With the exception of business, cause we need to create a folder with this name: Exemple: 

server/config/routes>private/"insurances.js"
server/app/controllersinsurances.js
server/app/modules/business/<>/<categoryName>.js

Routes

// Configurações
'use strict';

const path = require('path');
const rootPath = path.normalize(__dirname + '/../../../');
const mdw = require(rootPath + 'config/middlewares/middlewares');
const express = require('express');
const router = express.Router();

var insurancesCtrl = require(rootPath + 'app/controllers/insurances');

module.exports = () => {

// Criando a rota
  router.get('/bff/insurance-manager/customer/insurances/:insurance_id/renewals',
    mdw.baseMiddlewares,
    mdw.shutdown,
    mdw.general,
    insurancesCtrl.<nome da controller>
  );

  return router;
}

Lembre-se de colocar as rotas específicas antes das genéricas, por exemplo:

1- /home/cards/insurances
2- /home/cards

Controllers:

// Configurações
'use strict';

var path = require('path');
var rootPath = path.normalize(__dirname + '/../../app/');
var InsurancesBS = require(rootPath + 'modules/business/insurances/insurances');
var errorHandler = require('./error-conta-digital');

// Criando a controller
exports.getRenewalInsuranceDetails = function (req, res) {
  var insurancesBs = new InsurancesBS(req);

  insurancesBs
    .getRenewalInsuranceDetails()
    .then(function (response) {
      res.json(response);
    })
    .catch(function (err) {
      errorHandler.errorCD(err, res);
    });
};

Business:

// Configurações:
'use strict';

var patch = require('patch');
var rootPath = path.normalize(__dirname + '/../../../../');
var config = require (rootPath + 'config/config');
const request = require('request-promise');

class Insurances {
  constructor(req) {
    this.user = req.user.current;
    this.req = req;
    this.params = this.req.params;
    this.body = this.req.body || {};
    this.query = this.req.query;
    this.accessToken = this.req.user.profile_access_token;
    this.accountCode = this.req.user.current.account_code;
    this.headers = {
      Authorization: 'Bearer ' + this.accessToken,
      'x-account-code': this.accountCode,
      'user-agent': this.req.headers['user-agent'] || '',
      'X-Client-User-Agent': this.req.headers['user-agent'],
      'X-Client-Machine': this.req.cookies.machine
    };
   
// Criando o business para rotas novas do GMS
   getRenewalInsuranceDetails() {
    let options = {
      uri: `${config.gms.domain}/insurance-manager/customer/insurances/${this.params.insurance_id}/renewals`,
      method: 'GET',
      json: true,
      headers: this.headers,
    };
    return request(options);
  }

module.exports = Insurances;


// Criando business para gn-base.
