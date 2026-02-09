
- 1 [VUE CLI](#vue-cli)
- 2 [Architecture](#architecture)
- 3 [Components Concepts](#components-concepts)
    - 3.1 [Creating a Component](#creating-a-component)
    - 3.2 [Importing and declaring Component Globally](#importing-and-declaring-component-globally)
    - 3.3 [Importing and declaring Component Locally](#importing-and-declaring-component-locally)
    - 3.4 [Using Component](#using-component)
    - 3.5 [Capturing Template Element](#capturing-template-element)
- 4 [Component API's](#Component-API's)
    - 4.1 [Options API](#options-api)
    - 4.2 [Composition API](#composition-api)
- 5 [Interpolation](#interpolation)
    - 5.1 [Text Interpolation](#text-interpolation)
    - 5.2 [Javascript Interpolation](#javascript-interpolation)
- 6 [Directives](#directives)
    - 6.1 [Bind Directive](#bind-directive)
    - 6.2 [Two Way Bind Directive](#two-way-bind-directive)
    - 6.3 [Conditional Directives](#conditional-directives)
    - 6.4 [Loop Directive](#loop-directive)
    - 6.5 [Event Binding (Event listener)](#event-binding-(event-listener))
    - 6.6 [Once Render Content](#once-render-content)
    - 6.7 [Render Static Content](#render-static-content)
    - 6.8 [Dinamic Content For Child Component](#dinamic-content-for-child-component)
    - 6.9 [HTML Dinamic Content](#HTML-dinamic-content)
- 7 [Class and Styles Bindings](#class-and-styles-bindings)
    - 7.1 [Binding Class](#binding-class)
    - 7.2 [Binding Styles](#binding-styles)
- 8 [Component Lifecycle](#component-lifecycle)


</br>
</br>
</br>

## VUE CLI

For create a new VUE project, we can use the VUE CLI to build a vue project architecture.

Access the link below and follow the steps::

<a href="https://cli.vuejs.org/" target="_blank">Official CLI Tutorial</a>


</br>
</br>
</br>

## Architecture

The architecture project:

- `node_modules`: All modules necessaries to run our application.
- `public`: All public and static files that make up our application.
    - `favicon`: icon files.
- `src/source`: 
    - `assets`: That we have our image and styles files.
    - `components`: Our vue components files.
    - `app.vue`: the main component vue file.
    - `main.js`: inside this file, we have a instance vue app.
    - `vue.config.js`: Special vue configs.
    - `package.json`: all scripts and dependencies rountines.
    - `package-lock.json`: Dependency version security lock.
    - `lint`: Here we configure the sintaxe patterns
    - `.gitignore`: Here we declare the files that don't send to our repository.

</br>
</br>
</br>

## Components Concepts

In VUE.js, everything is a component. And these components are Single File Component (SFC), his maske up 
with:

- **TEMPLATE**: In template is our our HTML structure
- **SCRIPT**: In script is our javascript code
- **STYLE**: In style is our CSS code.

</br>

### Creating a Component

In Component folder, create a new .vue file. 
The name would be named with <ins>two words</ins>, with <ins>PascalCase</ins>. For example:

`TheHeader.vue`
`SubmmitButton.vue`

</br>

### Importing and declaring Component Globally

If you use the same component, at all or almost pages. We can import the component globally. 
In <ins>main.js</ins> file, use the <ins>.component()</ins> method:

    import {createApp} from 'vue'
    import TheHeader from '.components/TheHeader.vue'
    import SubmmitButton from './components/SubmmitButton.vue'

    const app = createApp({})

    app.component('TheHeader', TheHeader)
    app.component('SubmmitBUtton', SubmmitButton)

    //or

    app
      .component('TheHeader', TheHeader)
      .component('SubmmitButton', SubmmitButton)

</br>

### Importing and declaring Component Locally

In a parent component, we need to import and declare de component that we want to use. Like this:

    // Option API

    <script>
      import TheHeader from './components/TheHeader.vue'
      import SubmmitButton from './components/SubmmitButton.vue'

      export default {
        components: {
          TheHeader,
          SubmmitButton
        }
      }
    </script>

    // Composition API

    <script setup>
      import TheHeader from './components/TheHeader.vue'
      import SubmmitButton from './components/SubmmitButton.vue'
    </script>

</br>

### Using Component

For using our component, use need to declare him inside of template, with <ins>kebab-case</ins>.Like this:

    <template>
      <the-header />
      <submmit-button />
    </template

Or:

    <template>
      <the-header></the-header>
      <submmit-button></submmit-button>
    </template>

<a href="https://vuejs.org/guide/components/registration.html" target="_blank">Official Documentation</a>

</br>

### Capturing Template Element

We can catch the HTML content for use and explore in javascript language (script).

`refs`: Wich refs we can select the HTML content with him values and parameters. For this, we use the **ref** parameter, and we named as we want. Example:

    <template>
      <input type="text" ref="input">
    </template>

After, we can use this HTML element to inspect and use.

`$`: The dollar sign is a special VUE property, and ever we wanna see some VUE propertie we needed to use. Example:

    <template>
      <input type="text" ref="input">
    </template>

    // Options API

    <script>
    export default {
      data() {
        return {
          content: ''
        }
      }
      mounted() {
        this.content = this.$refs.input
      }
    }
    </script>

    // Composition API (we don't need use the $)

    <script setup>
    import { ref, onMounted } from 'vue'

    // the name of data must match template ref value
    const input = ref(null)

    onMounted(() => {
      content = input
      console.log(content)
    })
    </script>
On this example, we have the HTML element content with your tags, and values. 

`dir`: With dir, we can specify the element diretory content. Example:

    <template>
      <input type="text" ref="input">
    </template>

    // Options API

    <script>
    export default {
      data() {
        return {
          content: ''
        }
      }
      mounted() {
        this.content = this.$refs.input
        console.dir(this.$refs.input)
      }
    }
    </script>

    // Composition API

    <script setup>
    import { ref, onMounted} from 'vue'
  
    const input = ref(null)

    onMounted(() => {
      content = input
      console.dir(content)
    })
    </script>

And with that, we can work with the directory. Example:

    <template>
      <input type="text" ref="input">
    </template>

    // Options API

    <script>
    export default {
      data() {
        return {
          content: ''
        }
      }
      mounted() {
        // value directory:
        this.content = this.$refs.input.value
        console.dir(this.$refs.input)
      }
    }
    </script>

    // Composition API 

    <script setup>
    import { ref, onMounted} from 'vue'

    const input = ref(null)

    onMounted(() => {
      content = input.value
      console.log(content)
    })
    </script>

<a href="https://vuejs.org/guide/essentials/template-refs.html#accessing-the-refs" target="_blank">Official Documentation</a>


</br>
</br>
</br>

## Component API's

On Vue 3, we have two ways to define the component, **Composition** and **Options**. Let's se each way.

</br>

### Options API

On the **Options API**, we have four main options for define our component. Let's check:

`data()`: Here we define our reactive datas, when we need to call some data in another field of our script, we call this
data with **this.** prefix.

    <script>
    export default {
      data() {
        return {

          // number
          number: 0

          // strings
          theString: 'some text',

          // boolean
          validated: false,

          // object
          someObject: {
            color: 'white',
            age: 21,
            name: Caio
          },
          
          // arrays lists
          theArray: [
            pineapple,
            apple,
            banana
          ]
        }
      }
    }
    </script>

</br>

`methods`: With methods, we define your functions and logics. We can call our method's on events, inside other methods, inside of template and hooks. Ever something change on the page, the methods are be called
</br>

**Use**: Use the to run logics whenever any change occurence on the page, on interpolation and events.

    <script>
    export default {
      data() {
        name: ''
      },
      methods: {
        changeName() {
          // Remember to use the "this." prefix
          this.name = 'Caio'
        }
      }
    }
    </script>

</br>

`computed`: Computed's properties, works like a methods, but computed should ever return something, can be called on templates as a data properties, but can't be called on template events, because Computed's are getters. Computed's are be recalculated if just some computed dependency changes (the dependencies are saving in cache).
</br>

**Use**: The computed's properties, works like a data properties. Use for derivate data based in another datas, when the de dependency data suffer some change.

    <script>
    export default {
      data() {
        name: 'Carlos',
        lastName: 'Fonseca'
      },
      computed: {
        fullName() {

          // name is a dependency
          if (this.lastName === '') {
            return this.name
          } else {
            return `${this.firstName} ${this.lastName}`;
          }
        }
      }
    }
    </script>

</br>

`watchers`: Watchers works watching some data our computed, for execute some logic, but don't to return another value based on the watched value. The objetive is execute some logic. The name should be the same name of the computed our data that being watched.
</br>

**Use**: Run in real time, ever the data changed. Use for any non-data updated your want to make. Named with the same name as the property being assisted. Recomended in the http requests.
</br>

**Params**: We can access the old and new value, setting the params.
</br>

**deep**: If you work with a object, and need that watch run when the nested property change, you need to use Deep, property:

    <script>
    export default {
      data() {
        name: '',
        showName: false,
      },
      watch: {
        name( newName, oldName ) {
          console.log('The new name is: ', newName, ', and the old name is: ', oldName)
          showName = true
        }
      }
    }
    </script>

    // With Deep property

    <script>
    export default {
      data() {
        user: {
          name: '',
          lastName: '',
        },
        showName: false,
      },
      watch: {
        name( newValue, oldValue ) {
          console.log('The new full name is: ', newValue.Name + newValue.lastName)
          showName = true
        },
        deep: true
      }
    }
    </script>

<a href="https://vuejs.org/api/options-state.html#options-state" target="_blank">Official Documentation</a>


### Compostion API

In the Composition API, we have some diferent approaches

`data() -> refs`: In composition API, data properties become a normal variables, but they are declared with **ref()**. And all of them, behind the scenes are objects.

**Use**:Here, we use the reactive data with simple form:

    <script>
    import { ref } from 'vue'

    export default {
      setup() {
      
        // user const, EVER
        const uName = ref('Caio Montenegro')

        setTimeout(() => {

          // Remember, here the datas was saved as object
          uName.value = 'Caio'
        })

        return { userName: uName}
      }
    }
    </script>

    <template>
      <h1>{{ uName }}</h1>
    </template>

For use with objects, we can use the **ref()**, but we can also user the **reactive()**, because he simplified the code. Let's see:

    // With refs()

    <script>
    import { ref } from 'vue'

    export default {
      setup() {
      
        const user = ref({
          name: "Caio Montenegro",
          age: 31
        })

        setTimeout(() => {
          user.value.name = 'Caio'
          user.value.age = 32
        })

        return { user: user}
      }
    }
    </script>

    // with reactive()

    <script>
    import { ref, reactive } from 'vue'

    export default {
      setup() {
      
        const user = reactive({
          name: "Caio Montenegro",
          age: 31
        })

        setTimeout(() => {
          
          // Here we don't need use the .value
          user.name = 'Caio'
          user.age = 32
        })

        return { user: user}
      }
    }
    </script>

Now, let's see the simplified code, with **Script Setup**, with ref() and reactive():


    <script setup>
    import { ref } from 'vue'

    const uName = ref('Caio Montenegro')

    setTimeout(() => {
      uName.value = 'Caio'
    })

    </script>

    <template>
      <h1>{{ uName }}</h1>
    </template>


    // with object

    <template>
      <h2>{{ user.name }}</h2>
      <h3>{{ user.age}}</h3>
    </template>

    <script setup>
    import { ref, reactive } from 'vue'
    
    const user = reactive({
      name: "Caio Montenegro",
      age: 31
    })

    setTimeout(() => {
      user.name = 'Caio'
      user.age = 32
    })

    </script>

</br>

`methods -> Regular Functions`: Here, we can use the simple functions, to substitute the methods, just like that:

**Use**: 

    <template>
    <button @click="setAge" ></button>
    </template>

    <script> 
    import { reactive } from 'vue'

    export default {
      setup() {
        const user = reactive({
          name: 'Caio',
          age: 31
        })

        function setNewAge() {
          user.age = 32
        }

        return { user: ser, setAge: setNewAge}
      }
    }
    </script>

    // Simplified


    <template>
    <button @click="setAge" ></button>
    </template>

    <script setup> 
    import { reactive } from 'vue'

    const user = reactive({
      name: 'Caio',
      age: 31
    })

    function setAge() {
      user.age = 32
    }

    </script>

</br>

`Computed`: let's see how we can use the computed:

    <script>
    import { reactive } from 'vue'

    export default {
      setup () {

        const customer = reactive({
          name: 'Caio Montenegro',
          books: [
            'Vinte Mil Léguas Submarinas', 
            'O Senhor dos Anéis',
            'Possessão'
          ]
        })

        // computed:
        const booksAcquired = computed(() => {
          return customer.books.length > 0 ? 'yes' : 'No'
        })

        return  {
          customer,
          booksAcquired
        }
      }
    }
      
    </script>

    // Simplified

    <script setup>
    import { reactive } from 'vue'

    const customer = reactive ({
      name: 'Caio Montenegro',
      books: [
        'Vinte Mil Légua Submarinas', 
        'O Senhor dos Anéis',
        'Possessão'
      ]
    })

    // computed:

    const booksAcquired = computed (() => {
      return customer.books.length > 0 ? 'yes' : 'no'
    })
    </script>

`Watch`: Finally let's see watchers:

    <script setup>
    import { reactive, watch } from 'vue';

    // Definindo um objeto reativo
    const user = reactive({
      name: 'Carlos',
      age: 30,
    });

    // Usando o watch com deep para observar alterações no objeto inteiro
    watch(user, (newVal, oldVal) => {
      console.log('Pessoa foi alterada:');
      console.log('Antes:', oldVal);
      console.log('Depois:', newVal);
    },{ deep: true });
    </script>


</br>
</br>
</br>

## Interpolation

We can use a reactive data and some logics, in our template component. For that we use the Interpolation, with
Mustache sintax (double curly braces).

</br>

### Text Interpolation

Using reactive data on your template. Example:

      <template>
        <span>{{ name }}</span>
      </template>

      // Options API

      <script>
        export default {
          data() {
            return {
              name: 'VUE 3'
            }
          }
        }
      </script>

      // Composition API

      <script setup>
      import { ref } from 'vue'
        const name = ref('VUE 3')
      </script>

We also use Objects, and Array lists in Mustache sintax.

</br>

### Javascript Interpolation

The interpolation, also accepts javascript language logics. Example:

  <ins>Concatenation:</ins>

    <template>
      <span>{{ name + '' + lastName}}</span>
    </template>

    // Options API

    <script>
      export default {
        data() {
          return {
            name: 'VUE 3',
            lastName: 'The Knowledge'
          }
        }
      }
    </script>

    <script setup>
    import { ref } from 'vue'
      const name = ref('VUE 3')
      lastName = ref('The Knowledge')
    </script>

  <ins>Ternary Expression:</ins>

      <template>
        <span>{{ positiveNumber ? 'positve' : "negative" }}</span>
      </template>

      //Options API

      <script>
        export default {
          data () {
            return {
              positiveNumber: True
            }
          }
        }
      </script>

      // Compostion API 

      <script setup>
      import { ref } from 'vue'
        const positiveNumber = ref(True)
      <script>



  <ins>Javascript methods and functions:</ins>

    <template>
      <span>{{ name.split('').reverse().join('') }}</span>
    </template>

    // Options API

    <script>
      export default {
        data() {
          return {
            name: 'Caio'
          }
        }
      }
    </script>

    // Composition API

    <script setup>
    import { ref } from 'vue'
      const name = ref('Caio')
    </script>

  <ins>Template String:</ins>

    <template>
      <span id="`${id}`">{{ name }}</span>
    </template>

    // Options API

    <script>
      export default {
        data() {
          return {
            id: 01,
            name: 'VUE 3'
          }
        }
      }
    </script>

    // Composition API

    <script setup>
    import { ref } from 'vue'
    const id = ref(01)
    const name = ref('VUE 3')
    </script>

<a href="https://vuejs.org/guide/essentials/template-syntax.html#text-interpolation" target="_blank">Official Documentation</a>

</br>
</br>
</br>

## Directives

Directives are be VUE instructions. lets see these instructions below:

</br>

### Bind Directive

Directive to use a reactive data, on html properties. With this directive we can use dinamic values in our properties.

`v-bind`: Use the data bind directive as prefix for another HTML property. Example:

    <template>
      <img v-bind:src="imgURL" alt="Image">
    </template>

    // Options API

    <script>
    export default {
      data() {
        return {
          imgURL: '/path/src/img/myImage.png'
        }
      }
    }
    </script>

    // Composition API

    <script setup>
    import { ref } from 'vue'
    const imgURL = ref('/path/src/img/myImage.png')
    </script>

<ins>shorthand</ins>: The shorthand is ":" and "." for **props** modifiers (for change DOM property, not only HTML value). Example:

    <template>
      <img :src="imgURL" alt="Image">

      // For props:

      <input :value.prop="someObject">
      // equivalent to
      <input .value="someObject">
    </template>

    // Options API

    <script>
    export default {
      data() {
        return {
          imgURL: '/path/src/img/myImage.png'
        }
      }
    }
    </script>

    // Composition API

    <script setup>
    import { ref } from 'vue'
    const imgURL: ref('/path/src/img/myImage.png')
    <script>

</br>



<ins>Dinamic Attribute Name</ins>: We also can use the dinamic attribute with data bind. Check below example:

    <button v-bind:[key]="value"></button>
    // or
    <button :[key]="value"></button>
    
    // Options API

    <script>
    export default {
      data() {
        return {
          key: 'age',
          value: 01,
        }
      }
    }
    </script>

    // Composition API

    <script setup>
    import { ref } from 'vue'
    const key = ref('age')
    const value = ref(01)
    </script>

</br>

### Two Way Bind Directive

The VUE offer us a directive to implement a two-way data binding, that is, the user receive some reactive data and he can change this data, and return him to system. The name of this directive is **v-model**.

`v-model`: Similar to the bind, but the user can change de value, and send him to the system on real time. It's extremely indicate to use on input data forms. 

  <ins>Text Input</ins>

    <template>
      <label for="name">Insert the name:</label>
      <input id="name" type="text" v-model="firstName"></input>
      {{ firstName }}
    </template>

    // Options API

    <script>
      export default {
        data() {
          return {
            firstName: 'Caio'
          }
        }
      }
    </script>

    // Composition API

    <script setup>
    import { ref } from 'vue'
    const firstName = ref('Caio')
    </script>

  Here, we've a simple form. The input value, is pre configured with "Caio", and the same data is render below the input. But if the user change de value in the input, automacally the firstName data, will be change. Let's check more examples:

  <ins>Select Input</ins>

    <template>
      <label for="country">Countries</label>
      <select id="country" v-model="country">
        <option value="Brazil">Brasil</option>
        <option value="Argentina">Argentina</option>
        <option value="Colombia">Colombia</option>
      </select>
      {{ country }}
    </template>

    // Options API

    <script>
      export default {
        data() {
          return {
            country: "Brasil"
          }
        }
      }
    </script>

    // Composition API

    <script setup>
    import { ref } from 'vue'
    const country = ref('Brasil')
    </script>

  <ins>Radio Input</ins>

    <template>
      <label for="theme">Theme color</label>
      <input v-model="theme" type="radio" value="White">White</input>
      <input v-model="theme" type="radio" value="Black">Black</input>
      {{ 'You chosed :', theme}}
    </template>

    // Options API

    <script>
      export default {
        data() {
          return {
            theme:'White'
          }
        }
      }
    </script>

    // Composition API

    <script setup>
    import { ref } from 'vue'
    const theme = ref('white')
    </script>

  <ins>Checkbox input 1/2</ins>
  For boolean data:

    <template>
      <label for="contract">Do you agree wit the terms?</label>
      <input id="contract" type="text" v-model="accepted">I agree</input>
      {{ accepted }}
    </template>

    // Options API

    <script>
      export default {
        data() {
          return {
            accepted: null
          }
        }
      }
    </script>

    // Composition API

    <script setup>
    import { ref } from 'vue'
    const accepted = ref(null)
    </script>

  <ins>Checkbox input 2/2</ins>
  For array list data:

    <template>
      <label for="colors">Choose your favorite colors</label>
      <input type="checkbox" value="blue" id="colors">blue</input>
      <input type="checkbox" value="red" id="colors">red</input>
      <input type="checkbox" value="green" id="colors">green</input>
      <input type="checkbox" value="yellow" id="colors">yellow</input>
      {{ 'Favorite Colors:', colors  }}
    </template>

    // Options API

    <script>
      export default {
        data() {
          return {
            colors: []
          }
        }
      }
    </script>

    // Composition API

    <script setup>
    import { ref } from 'vue'
    const colors = ref([])
    </script>

</br>

### Conditional Directives

These directives, will show some content based on some condition.

`v-show`: Use for show some content if the condition is <ins>TRUE</ins> or <ins>FALSE</ins>. Example:

    <template>
      <span v-show="showText" >Hello world</span>
    </template>

    // Options API

    <script>
    exporta default {
      data() {
        return: {
          showText: true
        }
      }
    }
    <script>

    // Compostion API 

    <script setup>
    import { ref } from 'vue'
    const showText = ref(True)
    </script?

  Or:

    <template>
      <span v-show="showText === textEnable" >Hellow world</span>
    </template>

    // Options API

    <script>
    export default {
      data() {
        return {
          showText: true
          textEnable:  true
        }
      }
    }
    </script>

    // Composition API

    <script setup>
    import { ref } from 'vue'
    const showText = ref(true)
    const textEnable = ref(true)
    </script>


The <nis>v-show,</nis> makes the content to be loaded in DOM, even if the condition is false. But he input a style: **dipslay: none;** if the condition was false.

</br>

`v-if`: Use for show some content if the condition is **TRUE** or **FALSE**. Example:

    <template>
      <span v-show="showText" >Hello world</span>
    </template>

    // Options API

    <script>
    export default {
      data() {
        return {
          showText: true
        }
      }
    }
    <script>

    // Composition API

    <script setup>
    import { ref } from 'vue'
    const showText = ref(true)
    </script>

The diference between **v-if** of **v-show**, that's **v-if** not be loaded at DOM, if the condition is not met.

</br>

`v-else-if`: Use for gives continue the condition logic, if you have more than one content based on the conditions you may have. Example:

    <template>
      <span v-if="text === primaryText">Hello World</span>
      <span v-else-if="text === secundaryText">Hello VUE 3</span>
    </template>

    // Options API

    <script>
    export default {
      data() {
        return {
          text: 'Hello VUE 3',
          primaryText: 'Hello World',
          secundaryText: 'Hello VUE 3'
        }
      }
    }
    </script>

    // Composition API

    <script setup>
    import { ref } from 'vue'
    const text = ref('Hello VUE 3')
    const primaryText = ref('Hello World')
    const secundaryText = ref('Hello VUE 3')ref(
    </script>

</br>

`v-else`: Use for show a content if the previous conditions is not be met. Exemple:

    <template>
      <span v-if="text === primaryText">Hello World</span>
      <span v-else-if="text === secundaryText">Hello VUE 3</span>
      <span v-else>Hello everyone</span>
    </template>

    // Options API

    <script>
    export default {
      data() {
        return {
          text: 'Hello VUE 3',
          primaryText: 'Hello World'
          secundaryText: 'Hello VUE 3'
        }
      }
    }
    </script>

    // Composition API

    <script setup>
    import { ref } from 'vue'
    const text = ref('Hello VUE 3')
    const primaryText = ref('Hellow World')
    const secundaryText = ref('Hello VUE 3')
    </script>

**Obs**: We necessarily need use **v-if** before, and exactly before using the **v-else** and **v-else-if**.

<a href="https://vuejs.org/api/built-in-directives.html" target="_blank">Official Documentation</a>

</br>

### Loop Directive

Directives for render the content, several times. For this, we have only one directive.

`v-for`: This directives render the content, several times, traversing some array. It is very important, that we use the **key** property tag, for add a key id, for each content that will be render. Examples:

    <template>
      <span v-for="user in names" key="name">{{ user }}</span>
    </tempalte>

    // Options API

    <script>
      export default {
        data() {
          return {
            names: ['Caio', 'Silvana', 'Evandro']
          }
        }
      }
    </script>

    // Composition API

    <script setup>
    import { ref } from 'vue'
    const names = ref(['Caio', 'Silvana', 'Evandro'])
    </script>

With Object:

    <template>
      <span v-for="user in users" :key="user.id">{{ user.name }}</span>
    </template>

    // Options API

    <script>
    export default {
      data() {
        return {
          users: [
            {id: 0, name: 'Caio'},
            {id: 1, name: 'Silvana'},
            {id: 2, name: 'Evandro'}
          ]
        }
      }
    }
    </script>

    // Composition API

    <script setup>
    import { reactive } from 'vue'
    const users = reactive([
      {id: 0, name: 'Caio'},
      {id: 1, name: 'Silvana'},      {id: 2, name: 'Evandro'}
    ])
    </script>

<a href="https://vuejs.org/api/built-in-directives.html#built-in-directives" target="_blank">Official Documentation</a>

</br>

### Event Binding (Event listener)

The directive for listen javascript events. 

`v-on`: With this directive, we can listen some javascript event and call a function to be executed, or so some javascript instruction. Example:

      <template>
        <button v-on:click="count++">Plus 1</button>
      </template>

      // Options API

      <script>
      export default {
        data() {
          return {
            count: 0
          }
        }
      }
      </script>

      // Composition API

      <script setup>
      const count = ref(0)
      </script>

<ins>shorthand</ins>: We can use a simple shorthand: "@"

      <template>
        <button @click="count++">Plus 1</button>
      </template>

      // Options API

      <script>
      export default {
        data() {
          return {
            count: 0
          }
        }
      }
      </script>

      // Composition API

      <script setup>
      const count = 0
      </script>

<a href="https://vuejs.org/guide/essentials/event-handling.html#listening-to-events" target="_blank">Official Documentation</a>

</br>

### Once Render Content

For render the content or element once only, use the **v-once**.

`v-once`: The content, will be render once only. If the element or component will be render again, the content do not be updated, even if the user change de value. Example:

    <template>
      <span> v-once> This will never change: {{msg}}</span>
      <input type:"text" v-model="msg"></input>
    </template>

    //options API

    <script>
    export default {
      data() {
        return {
          msg: ''
        }
      }
    }
    </script>

    //composition API

    <script setup>
    let msg = ''
    </script>

<a href="https://vuejs.org/api/built-in-directives.html#v-once" target="_blank">Official Documentation</a>

</br>

### Render Static Content

For render the static content.

`v-pre`: even you use mustache tags, the content will be render as-is. Example:

    <template>
      <span>The mustache tags, should be used for render the dinamic content {{ dinamic content }}</span>
    </template>

<a href="https://vuejs.org/api/built-in-directives.html#v-pre" target="_blank">Official Documentation</a>

</br>    

### Dinamic Content For Child Component

For render a dinamic HTML/string content in a component child, that we call. We can use **slots**.

`v-slot`: Pass the dinamic template content (HTML) for child component. Check this example beloow, supose that we have a simple layout, that we need to render a section title.

    // Parent Component

    <template>
      <child-component>
        <template v-slot>
          My Section Title
        </template>
      </child-component>
    </template>

    // Child Component (called)

    <template>
      <h1>
        <slot></slot>
      </h1>
    </template>

<ins>Named Slots:</ins>
We can use multiple slot, and also specify the slot by naming it. Example:

    // Parent Component
  
    <template>
      <child-component>
        <template v-slot:title>
          My Title
        </template>
        <template v-slot:content>
          This is the content
        </template>
      </child-component>
    </template>

    // Child Component

    <template>
      <h1>
        <h1>
          <slot name="title"></slot>
        </h1>
        <h2>
          <slot name="sub-title"></slot>
        </h2>
        <div>
          <slot name="content"></slot>
        </div>
      </h1>
    </template>

On above example, we can use only slots that we need.

<ins>Shorthand:</ins> The short hand for slots is <b>#</b> by named slots. If slot don't have name, use <b>#default</b>.

<ins>Scoped Slots:</ins>
With scoped, we can pass child data to the parent. Example:

    // Parent Component

    <template>
      <child-component :items="items">
        <template #item="slotProps">
          <div>{{ slotProps.item.name }}</div>
        </template>
      </child-component>
    </template>

    // Child Component

    <template>
      <div>
        <slot v-for="item in items" :item="item"></slot>
      </div>
    </template>

    // Options API

    <script>
    export default {
      data() {
        return {
          items:['apple', 'banana']
        }
      }
    }
    </script>

    // Composition API

    <script>
    const items=['apple', 'banana']
    </script>

<a href="https://vuejs.org/api/built-in-directives.html#v-slot" target="_blank">Official Documentation</a>

</br>

### HTML Dinamic Content

For render html tags, contained in string value, we can use a simple, but dangerous directive.

`v-html`: Use this tag, for leave tag contained in strings comply your functions. Examples:

    <template>
      <div v-html="goal">
      </div>
    </template>

    // Options API

    <script>
    export default {
      data() {
        return {
          goal: 'Learn Vue 3'
        }
      }
    }
    </script>

    // Composition API

    <script setup>
    const goal = 'Learn Vue 3'
    </script>

**Caution**: v-html allow the user to input HTML content in your app. Use with care.

<a href="https://vuejs.org/api/built-in-directives.html#v-html" target="_blank">Official Documentation</a>

</br>
</br>
</br>

## Class and Styles Bindings

The VUE offer us a simple way to apply Dinamic Classes and Styles: Class and Style Bindings. For apply the dinamic class and styles, we'll use the [Data Bindin Concepts](#Bind-Directive).

</br>

### Binding Class

For apply the dinamic class, with bind is much simple. Look the below example:

    <template>
      <h1 :class="title" >Hello VUE 3</h1>
    </template>

    // Options API

    <script>
    export default {
      data() {
        return {
          title: 'titleStyle'
        }
      }
    }
    </script>

    // Composition API

    <script setup>
    const title = 'titleStyle'
    </script>

    <style>
    .titleStyle {
      color: blue;
    }
    </style>

When we use data bind in **class** or **styles** attributes, the **v-bind** suport **objects** and **arrays** as a value. And set some logics for use dinamic class and styles. 
Class with object example:


    <template>
      // title = class name
      // true = condition for apply the class, received from reactive data.
      <h1 :class="{ 'title': true }">Hello Vue</h1>
    </template>

    // More than one class

    <template>
      <h1 :class="{ 'title': true, homeTitle: false, subTitle: true}">Hello Vue</h1>
    </template>

    // IMPORTANT: The last classes declared subscribe the first classes

Class with array example:

    <template>
      // title = class name
      // true = condition for apply the class
      <h1 :class="['title', titleHome]">Hello Vue</h1>
    </template>

    // IMPORTANT: The last classes declared subscribe the first classes

Class with array and object example:

    <template>
      // title = class name
      // true = condition for apply the class
      <h1 :class="['title', {'titleHome': true}]">Hello Vue</h1>
    </template>

    // IMPORTANT: The last classes declared subscribe the first classes

**Tip**: We can transfer the attribute content to reactive data:

    <template>
      // title = class name
      // true = condition for apply the class
      <h1 :class="classList">Hello Vue</h1>
    </template>

    // Options API

    <script>
    export default {
      data() {
        return {
          classList=['title', {'titleHome': true}]
        }
      }
    }
    </script>

    // Compostion API

    <script setup>
    const classList = ['title', {'titleHome': true}]
    </script>

    // The same logic is valid for Objects.

We can apply some logic dinamic class when we use array format with **Ternary Expression**. Like that:

    <template>
      // isActive = reactive boolean data
      // activeClass = If true, apply activeClass
      // '' = If False, don't apply classe
      <span :class="[isActive ? activeClass : '', errorClass]">
        Hello Vue 3
      </span>
    </template>

</br>

### Binding Styles

The logic for apply dinamic styles on our component is the same such **dinamic classes**, but here we use only object value, and instead of using class name as a value, we'll use the css properties. Example:

    <template>
      <h1 :style="{'color': primaryColor, 'background-color': secundaryColor}">Hello VUE3</h1>
    </template>

    // Options API

    <script>
    export default {
      data() {
        return {
          primaryColor: 'blue',
          secundaryColor: 'black'
        }
      }
    }
    </script>

    // Compostion API

    <script setup>
    const primaryColor = 'blue', 
    const secundaryColor = 'black'
    </script>

    // or 

    <template>
      <h1 :style="styleClass">Hello VUE3</h1>
    </template>

    // Options API

    <script>
    export default {
      data() {
        return {
          styleClass={'color': primaryColor, 'background-color': secundaryColor}
          // or
          styleClass={color: primaryColor, backgroundColor: secundaryColor}
        }
      }
    }
    </script>

    // Compostion API

    <script setup>
    const styleClass={'color': primaryColor, 'backgournd-color': secundaryColor}
    // or
    const styleClass={color: primaryColor, backgroundColor: secundaryColor}
    </script>

<a href="https://vuejs.org/guide/essentials/class-and-style.html#class-and-style-bindings" target="_blank">Official Documentation</a>

</br>
</br>
</br>

## Component Lifecycle

Each component instance has a cycle, that we can use to input functions with our instructions. Bellow we
can see the order:

- --> Init Composition API
- 1 - [beforeCreate](#beforeCreate)
- --> Init Options API
- 2 - [created](#created)
- 3 - [beforeMount](#beforeMount)
- 4 - [mounted](#mounted)
  - 4.1 - [beforeUpdated](#beforeUpdated)
  - 4.2 - [updated](#updated)
- 5 - [beforeUnmount](#beforeUnmount)
- 6 - [unmounted](#unmounted)

</br>

### beforeCreate

All routines declared here, will be executed before component is created. That is, when the component has instanced, before Vue has set up the component's data, computed, methods, and event listeners. Before create is available only on Options API. 

    // Options API

    <script>
    export default {
      beforeCreate() {
        console.log('Component has been instanced')
      }
    }
    </script>

</br>

### created

The routines that will be declared here, will be declared after the component is initialized. So VUE component has already set up the component's data, computed, methods, and events listeners. Before create is available only Options API.

    // Options API

    <script>
    export default {
      created() {
        console.log('Component has been created')
      }
    }
    </script>

</br>

### beforeMount

Here, the function and instructions will be executed, before the component is added to the DOM.

    // Options API

    <script>
    export default {
      beforeMount() {
        console.log('Component is already to be mount')
      }
    }
    </script>

    // Composition API

    <script setup>
    import {onBeforeMount}
    
    onBeforeMount(() => {
      console.log('Component is already to be mount')
    })
    </script>

</br>

### mount

Right after a component is added to the DOM tree, the **mounted** function is called.

    // Options API

    <script>
    export default {
      mounted() {
        console.log('The component was mounted')
      }
    }
    </script>

    // Composition API

    <script setup>
    import { onMounted } from 'vue'

    onMounted(() => {
      console.log('The component was mounted')
    })
    </script>

</br>

### beforeUpdate

Is called whenever there is a change in the data fof your component, but before the update is rendere to the screen.

    // Options API

    <script>
    export default {
      beforeUpdate() {
        console.log('Some data or content will be change and uptade')
      }
    }
    </script>

    // Compostion API

    <script setup>
    import { onBeforeUpdate } from 'vue'
    onBeforeUpdate(() => {
      console.log('Some data ofr content will be change and update')
    })
    </script>

</br>

### updated

This hook is called after our component has updated it's DOM tree.

    // Options API

    <script>
    export default {
      updated() {
        console.log('The component has been updated in DOM')
      }
    }
    </script>

    // Composition API

    <script setup>
    import { onUpdated } from 'vue'

    onUpdated(() => {
      console.log('The componenthas been updated in DOM')
    })
    </script>

</br>

### beforeUnmount

This hook is called just before a componet is removed from the DOM

    // Options API

    <script>
    export default {
      beforeUnmount() {
        console.log('This component will be unmount of DOM')
      }
    }
    </script>

    <script setup>
    import { onBeforeUnmount } from 'vue'

    onBeforeUnmount(() => {
      console.log('This component will be unmount of DOM')
    })
    </script>

</br>

### unmounted

This hook is called when the component is removed from the DOM tree.

    // Options API

    <script>
    export default {
      unmounted() {
        console.log('The component has been removed from the DOM')
      }
    }
    </script>

    // Composition API

    <script setup>
    import { onUnmounted } from 'vue'

    onUnmounted(() => {
      console.log('The component has been removed from the DOM')
    })
    </script>


<a href="https://vuejs.org/api/options-lifecycle.html" target="_blank"> Official Option API Documentation</a>
</br>
<a href="https://vuejs.org/api/composition-api-lifecycle.html" target="_blank">Official Composition API Documentation</a>

</br>
</br>
</br>


