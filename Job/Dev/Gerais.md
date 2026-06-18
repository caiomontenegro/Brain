### 📋 Etapa 1 — Reduzir o tempo de execução de JavaScript (2,3s)


 **Chat Salesforce**
   carregado no  **`onMounted`**  do layout do arquivo: z:\portal-frontend\src\layouts\default.vue
   
   ```
   window.chatSalesforce.initGenia({ launchChat: false })`
   ```

e é chamado em toda página, carregando o script Salesforce imediatamente no load. E dentro do  ``initGenia`` ele:

1.  Faz um fetch do script externo da Salesforce com ``Date.now()`` como cache-buster — ou seja, nunca cacheia
2. Instancia o ``embeddedservice_bootstrap``
3. Injeta um iframe no DOM.


A solução mais simples e eficaz é adiar esse init usando ``requestIdleCallback``, que só executa quando o browser está ocioso — depois que os elementos críticos já renderizaram:

```
// ANTES
window.chatSalesforce.initGenia({ launchChat: false });

// DEPOIS
const initChat = () => window.chatSalesforce.initGenia({ launchChat: false });

if ('requestIdleCallback' in window) {
  requestIdleCallback(initChat, { timeout: 5000 });
} else {
  setTimeout(initChat, 3000); // fallback para Safari
}
```

 **Google Fonts**
 Está carregando via ```<link rel="stylesheet">``` bloqueante () — O CSS da Google Fonts bloqueia rendering e executa parser.

 **GTM**
 GTM carregado no evento ``load`` — embora esteja no window.addEventListener('load'), ainda adiciona JS pesado durante o tempo crítico de interação.

**Flowbite**
registrado como plugin global () — carrega a lib inteira na inicialização, mesmo que a homepage não use todos os componentes Flowbite.


**lottie-web**
importado sincronamente no componente — mesmo que o componente não esteja na home, ele está registrado globalmente.


**@vueuse/motion**
aplicado em todo o app via módulo Nuxt — processa todas as diretivas ``v-motion`` na renderização inicial.

____


### 📋 Etapa 2 — Minimizar o trabalho da thread principal (3,8s)


**Componentes registrados globalmente** 
Todos os componentes na pasta components/ são registrados globalmente () — Nuxt auto-importa e resolve todos esses componentes no startup.

**10 sections da home carregadas de forma síncrona**
Todas as 10 sections são renderizadas no primeiro paint, mesmo as que estão fora da viewport.
    
**useScroll com watch**
useScroll com watch no layout () — Executa em cada pixel scrollado sem throttle/debounce.

**useResizeObserver no menu**
Fires continuamente em resizes.

**processResize**
processResize sem debounce no layout — ``window.addEventListener('resize', processResize)`` sem throttle.


---

### 📋 Etapa 3 — Reduzir JavaScript não usado (671 KiB de economia)



**flowbite**
Registrado globalmente, mas usado apenas em componentes específicos (accordion, tooltip).

**swiper**
Presente no package.json, provavelmente carregado mesmo em páginas sem carousel.

**lottie-web**
Lib pesada importada sincrona no componente global.

**crypto-js**
No package.json, possivelmente usado em poucos lugares.

**visitdata plugin**
Carregado em todas as páginas.

**vue-odometer + vue-3-odometer + odometer**
Três libs para o mesmo propósito, registrado globalmente.


---

### 📋 Etapa 4 — Reduzir CSS não usado (125 KiB de economia)


**Flowbite CSS**
O plugin injeta estilos para todos os componentes (modals, dropdowns, tooltips, etc.) mesmo que não usados

**vue-final-modal/style.css**
importado globalmente () — Carrega CSS do modal em toda página.

**odometer-theme-default.css**
importado globalmente no plugin.

**Tailwind purgando parcialmente** — O 
O content no tailwind.config.js inclui ``node_modules/flowbite/**/*.js`` , o que faz o Tailwind gerar classes extras usadas internamente pelo Flowbite.

**Icon font com ~170 ícones**
Todos os glifos estão presentes, mesmo que apenas ~20 sejam usados na home

