# Vue.js 3

**Vue.js** is a javascript/typescript framework. It's popular for being approachable, versatile and performant and is used for making standalone widgets or web applications.

### Vue 3 New Features

- **The Composition API** - code reusability, organization and readability
- Multiple root elements inside template
- **Teleport component** - render content from one component in a different place in the DOM (modals)
- **Suspense Component**
  - used to handle asynchronus components
  - can provide fall-back content (spinner) until data is loaded
- Provides Typescript support

## Index

- [Add Vue using CDN](#addVueCdn)
- [Create Vue project](#createProject)
- [Component](#component)
- [Lifecycle hooks](#lifecycleHooks)
- [Vue.js devtools](#devtools)
- [Template syntax and Expressions](#syntax)
- [List rendering](#list)
- [Form input bindings](#inputBinding)
- [User events](#userEvents)
- [Methods](#methods)
- [Conditional rendering](#conditional)
- [Attribute binding](#attributeBinding)
- [Dynamic CSS classes](#dynamicCssClass)
- [Computed Properties](#computedProperties)
- [Template refs](#templateRefs)
- [Styling](#styling)
- [Props](#props)
- [Emitting custom events](#customEvents)
- [Event modifiers](#eventModifiers)
- [Key modifiers](#keyModifiers)
- [System modifiers](#systemModifiers)
- [Mouse button modifiers](#mouseBtnModifiers)
- [Slot](#slot)
- [Teleport](#teleport)
- [Router](#router)
- [Composition API](#compositionApi)
- [Vuex Store](#vuexStore)

<a name="addVueCdn"></a>

## Add Vue using CDN

This script needs to be added in our html file.

```html
<script src="https://unpkg.com/vue@3"></script>
```

- For creating an app and mounting it to a certain part of the app, write the div-id inside the **mount** method to control whatever is inside that div with Vue.

  ```html
  <script>
    const appName = Vue.createApp({
      data() {
        return {
          header: "Vue is ready!",
        };
      },
    }).mount("#div-id");
  </script>
  ```

  The app can also be created in a separate js file and linked with a script inside the <body> tag.

  ```html
  <script src="srcFileName.js"></script>
  ```

- For displaying this data in the page we can use the double mustache syntax. Remember that the variables created in **data** can only be accessed inside the div where we mounted the app.
  ```html
  <div id="div-id">
    <h1>{{header}}</h1>
  </div>
  ```
- To check out Vues **reactivity system**, we can create an input field and use Vues v-diective model that helps in **two-way data binding** meaning if you change the input, the header's gonna change and if you change the header, the input's gonna change. It can also be manipulated from the console.
  ```html
  <input v-model="header" />
  ```

<a name="createProject"></a>

## Create project

- Install nodejs and vue/cli globally.
  ```console
  $ sudo apt update
  $ curl -sL https://deb.nodesource.com/setup_14.x | sudo -E bash -
  $ sudo apt install nodejs
  $ node -v
  $ npm -v
  $ sudo apt install build-essential
  $ sudo npm i @vue/cli -g
  ```
- Create the project in your desired directory.
  ```console
  $ vue create project_name
  ```
- Run the project
  ```console
  $ cd project_directory
  $ npm run serve
  ```

<a name="component"></a>

### Component

Each Vue component can have 3 parts. A component must have a template, the other 2 are optional.

- An html template
- **script** part for exporting the component, importing other components. Here we can define Vue options like **data**, **methods**, **props** etc.
- **style** part for styling the component. By default, these styles are global.

Here's how the component tree of a project with multiple component looks like.
![Component tree](./assets/component_tree.png "Component Tree")

<a name="lifecycleHooks"></a>

### Vue.js lifecycle hooks

[Vue lifecycle diagram](https://v3.vuejs.org/guide/instance.html#lifecycle-diagram)

- **beforeCreate** - this is fired before the creation of the component. We can't access any data or templates here.
- **created** - this is fired after the component has been created. Only templates can be accessed from here.
- **beforeMount** - this is fired after the compilation and just before mounting the app. Here we can access all data, events and templates.
- **mounted** - this is fired after the component is mounted. Most **fetch** requests are created here, but it can be done in created or beforeMount hooks too.
- **beforeUpdate** - this is fired before re-rendering changed data to the DOM.
- **updated** - after updating the data to the DOM, this hook is fired.
- **beforeUnmount** - this is fired before unmounting the component.
- **unmounted** - this is fired after the component unmounts.

<a name="devtools"></a>

### Vue.js devtools

We need to install the **beta version(version 6)** of the **Vue.js devtools** extenion from the chrome web store. The beta version is not available for firefox yet. Then we need to go to manage extensions for this and check **Allow access to file URLs**.

- It injects our Vue intances into the console for us so that we can test and manipulate them without relying on setting them to a variable.
- Helps to keep up with our routes
- Helps to keep up with our Vuex store

<a name="syntax"></a>

### Template syntax and expressions

For separete js file, the html can be written inside the **template** option that Vue provides.

```js
template: "<h2>This is the template</h2>";
```

- js functions can be used inside the double mustache
- Only 1 expression is allowed
- Variables can't be declared and if statements aren't allowed
- Ternary expression is allowed, as well as OR

<a name="list"></a>

### List rendering in Vue 3

- We can make an array in the data and render it using **v-for** loop. A unique key should be used for items. It also supports objects.
  ```js
  listName: [
    { id: 1, label: "item 1" },
    { id: 2, label: "item 2" },
    { id: 3, label: "item 3" },
  ];
  ```
  ```html
  <ul>
    <li v-for="(item, index) in listName" :key="item.id">
      {{index}} {{item.label}}
    </li>
  </ul>
  ```
- To check out these list items from the console, we can write
  ```console
  $vm.data.listName
  ```

<a name="inputBinding"></a>

### Form input bindings

- **v-model** supports modifiers like **lazy, number, trim**.
  - lazy > it syncs the data after change events instead of each input event
  - number > it typecasts the user input a number
  - trim > trims whitespaces from the input
  ```html
  <input type="text" v-model.lazy="newItem" placeholder="Add an item" />
  ```
- It can be used with **text, multiline text, checkbox, radio, select**

<a name="userEvents"></a>

### User Events

**v-on** lets us respond to every event that javascript can. It supports **event modiefiers** and **key modifiers**. The shorthand syntax for v-on is **@**.

- v-on for click events.
  ```html
  <button v-on:click="methodName" class="btn btn-secondary">Add Item</button>
  ```
- v-on with key modifier.
  ```html
  <input
    @keyup.enter="methodName"
    type="text"
    v-model="newItem"
    placeholder="Add an item"
  />
  ```
- Vue provides an event parameter by default to the methods that we use with user events. If we want to pass both the event paramater and another custom parameter in the method, it should be written like this -
  ```html
  <div class="box" @mouseover="handleEvent($event, 5)">mouseover (enter)</div>
  ```

<a name="methods"></a>

### Methods

Vuejs has an option named **mathods** for writing methods. Methods are used for manipulating data while Computed properties are used for transforming them.

```js
methods: {
  methodName(){
    this.items.push({
      id: this.items.length + 1,
      label: this.newItem})
      this.newItem = ""
  }
}
```

<a name="conditional"></a>

### Conditional Rendering

- **v-if**, **v-else**, **v-else-if** and **v-show** is used for conditional rendering of elements.
  ```html
  <button v-if="property_name_for_condition" @click="doEdit(false)">
    Cancel
  </button>
  <button v-else @click="doEdit(true)">Add Item</button>
  <button v-show="property_name_for_condition">Show</button>
  ```
- **v-show** works by toggling an elements **display** css property meaning the element is always present in the DOM. **v-if** removes the element from the DOM if the condition is not satisfied.

<a name="attributeBinding"></a>

### Attribute Binding

**v-bind** is used to bind attributes to elements. The shorthand syntax for this is **:**.

```html
<button v-on:click="saveItem" v-bind:disabled="newItem.length === 0">
  Save Item
</button>
```

<a name="dynamicCssClass"></a>

### Dynamic CSS classes

- There are 2 ways for adding dynamic classes from the main.css file. It's possible to toggle multiple classes with both of these syntaxes.
  - **Object syntax**
    ```html
    <li
      v-for="(item, index) in items"
      :key="item.id"
      :class="{class_name: property_of_the_item}"
    >
      {{item.label}}
    </li>
    ```
  - **Array syntax**
    ```html
    <li
      v-for="(item, index) in items"
      :key="item.id"
      :class="[property_of_the_item ? 'class_name_1' : 'class_name_2']"
    >
      {{item.label}}
    </li>
    ```
- For adding a regular non-dynamic class to an element, we can use the **class** property or pass a string to our bound classes.
  ```html
     <li
      v-for="(item, index) in items" :key="item.id"
      class="static_class"
      :class="[property_of_the_item ? 'class_name_1' : 'class_name_2']>
      {{item.label}}
     </li>
  ```
  ```html
  <li
    v-for="(item, index) in items"
    :key="item.id"
    :class="[property_of_the_item ? 'class_name_1' : 'class_name_2',
              'static_class']"
  >
    {{item.label}}
  </li>
  ```

<a name="computedProperties"></a>

### Computed Properties

- The option for writing computed properties is **computed**.
- They're used only for tranforming data for the presentation layer, that's why it's recommended to use a spread operator so that we don't accidentally manipulate any data here.
- They can re-render themselves.
  ```html
  <p>{{characterCount}}/200</p>
  ```
  ```js
  computed: {
      characterCount(){
          return this.newItem.length
      }
  }
  ```

<a name="templateRefs"></a>

### Template refs

It allows us to store a reference of a DOM element inside a variable for manipulating that element using javascript methods.

```html
<template>
  <input type="text" ref="name" />
  <button @click="handleClick">Click</button>
</template>
```

```js
handleClick(){
    console.log(this.$refs.name)
    this.$refs.name.focus()
}
```

<a name="styling"></a>

### Styling

- For any global styling, make a global.css file in the assets folder and import it into the main.js file.
- For setting custom styles for components -

  - we can use the **scoped** property in style tag like this<style scoped>. The way it works is that some random data attribute is added to the style tags and the html elements that use the styles of that class so it appears different than the global styles.
  - make the class names more specific to that component. For example, for a Modal class the styling for h1 can be like this -

  ```css
  .modal h1 {
  }
  ```

<a name="props"></a>

### props

props are needed to make reusable components and to have a single source of truth in an app. For passing a prop, declare it in the <script> of the component you want to recieve it in. This is used for passing simple data.

```js
prop: ["header"];
```

Declare the prop in the data option of the parent element and bind it to the child element.

```html
<ChildComponent :header="header" />
```

<a name="customEvents"></a>

### Emitting custom events

Custom events are used to fire an event in the child component to change something in the parent component.
Make a method in the child component where the custom event is declared. Custom events can take extra data as parameter. It is recommended that the event names should be written in kebab-case.

```js
methodName() {
    this.$emit("custom-event-name")
    this.$emit("custom-event-name", data)
}
```

In the parent component, bind the custom event with the method you want to call.

```html
<ChildComponent @customEventName="methodName" />
```

<a name="eventModifiers"></a>

### Event modifiers

- **.stop** - the events propagation will stop.
- **.prevent** - prevents the events default behavior.
- **.capture** - an event targeting an inner element is handled here before being handled.
- **.self** - only trigger handler if event.target is the element itself.
- **.once** - trigger the event at most once.
- **.passive** - triggers the events default behavior.

<a name="keyModifiers"></a>

### Key modifiers

Key modifiers can be used with the keyboard events **@keyup**, **@keydown** and **@keypress**. The commonly used key aliases provided by Vue are -

- **.enter**
- **.tab**
- **.delete**
- **.esc**
- **.space**
- **.up**
- **.down**
- **.left**
- **.right**

<a name="systemModifiers"></a>

### System modifiers

These are for mouse or keyboard events.

- **.ctrl**
- **.alt**
- **.shift**
- **.meta**
- **.exact** - allows control of the exact combination of system modifiers needed to trigger an event. For example -
  ```html
  <button v-on:click.ctrl.exact="onCtrlClick">Button</button>
  ```
  This event will only fire when only ctrl is pressed.

<a name="mouseBtnModifiers"></a>

### Mouse button modifiers

- **.left**
- **.right**
- **.middle**

<a name="slot"></a>

### slot

They're useful for passing custom templates into components.

- For general slot, write a template you want to pass inside your component tag where the slot will show. Then add <slot></slot> in the template of that component. You can pass a default value inside your slot in case your slot content doesn't show.
  ```html
  <ComponentName>
    <h1>Slot</h1>
  </ComponentName>
  ```
  ```html
  <template>
    <slot>default content</slot>
  </template>
  ```
- For **named slot**, write your template structure inside a <template> tag inside your Component tag and give your template a name using the **v-slot** directive. Then add <slot></slot> with its name attribute in the template of that Component to specify which slot you want to show there.
  ```html
  <ComponentName>
    <template v-slot:slotName>
      <h1>Named slot</h1>
    </template>
  </ComponentName>
  ```
  ```html
  <template>
    <slot name="slotName"></slot>
  </template>
  ```

<a name="teleport"></a>

### Teleport

This component can be used to render content in a different place of the DOM.
For example, if we want to render a component in a custom div outside of the main div in index.html, we need to first write the div in index.html with a different id or class.

```html
<div id="customDivId"></div>
```

Then change the <div> tag of the div you want to teleport to <teleport> and add the **to** attribute to specify the div id or div class you want to teleport to. if you use the id then use **#** and if you use the class, use **.**.

```html
<teleport to="#customDivId">
  <ComponentName />
</teleport>
```

<a name="router"></a>

### Router

Vue.js automatically sets up the routing files for a project if the **Router** feature is selected manually at the start of project creation. The **history mode** for router should also be selected. After project creation we'll see that -

- There's a folder named router that consists of an **index.js** file. This file contains all the routes for the project. The **path** property is not case-sensitive.
- The routes are also defined in the **App.vue** file with **<router-link>** tag. For better maintainability, the routes should be declared using their **name** attributes.
- All the pages that have a routing link should be inside the **views** folder while the reusable components that are not page specific should be inside the **components** folder. The components that work on the same page should be inside separate folders for readability.
- If we don't select the Router option when creating the app, we can also set up the router ourselves by installing the **vue-router** package.

#### Route parameter

- used for nested routes. For example: **routeName/:paramName**. It can be accessed inside a component by writing **$route.params.paramName**.
- The parameter should be passed inside a <router-link> in this way.
  ```js
  <router-link :to="{ name: 'PathName', params: { paramName: param } }">
        <h2>{{ Link name }}</h2>
  </router-link>
  ```
- Route parameters can be passed as **props** in a component. In this case the **props** property should be set to true in the route object of that component in the index.js file.

  ```js
  {
    path: "/path",
    name: "PathName",
    component: ComponentName,
    props: true,
  }
  ```

#### Navigation

- A path can be redirected by using the **redirect** property of the route object.
  ```js
  {
    path: "/path",
    redirect: "/redirect-path"
  }
  ```
- For catching all the routes that don't exist, a not found component should be made and it's path should be set to **/:catchAll(.\*)**.

  ```js
  {
    path: "/:catchAll(.*)",
    name: "PathName",
    component: ComponentName,
  }
  ```

- The router object also provides methods to redirect, navigate backwards or forward inside a component.
  - **redirect**:
  ```js
  $router.push({ name: "PathName" });
  ```
  - **navigate backwards/forward**:
  ```js
  $router.go(-1);
  $router.go(1);
  ```

<a name="compositionApi"></a>

### Composition API

Generally we use the **Options API** provided by Vue to create components where variables, methods, computed properties all have to be written in separate options.

Composition API offers a **setup** hook where all of the functionalities needed to create a component can be written in one place, inside the setup hook, kind of like render in react.

- The **setup hook** runs before any other hooks
- we can declare variables and methods inside it
- Variables declared inside are not reactive like variables in data component. So to make the variables reactive, we can use **Template refs** by importing **ref** from **vue**. These variables can be accessed by their names in the template and by variable_name.value in the script.
- There's another alternative to make variables reactive in setup. That is by writing the variables inside **reactive**. But one thing to note is that**primitive values** don't work with reactive.
- To use any of the variables or methods inside the template, we have to return them from setup.

  ```js
    setup() {
      const varName = ref(value);
      const methodName = () => {
        //method body
      }

      return { varName, methodName }
    }
  ```

- **this** keyword is not available in setup
- **computed properties** can be used in setup using the **computed** function. **watch** and **watchEffect** can also be used in this way.

  ```js
  const methodName = computed(() => {
    return names.value.filter((name) => name.includes(search.value));
  });

  const stopWatch = watch(property_to_watch, () => {
    console.log("watch ran");
  });

  const stopWatchEffect = watchEffect(() => {
    console.log("watchEffect ran", property_to_watch.value);
  });
  ```

- **watch** function takes what to watch as an argument and calls a function if that property changes. The **watchEffect** function runs initially once. Both of these watchers have to be stopped manually.
- We can use **props** in setup using **setup(props)**.
- To use lifecycle hooks inside **setup**, we needto use **on** before the name of each hook and import the hook from vue. For example, **onMounted**. Lifecycle hooks can also be used like before outside the setup hook.

  ```js
  onMounted(() => console.log("Component Mounted"));
  ```

#### Reusable Composable functions

We can write reusable functions to use with the setup hook. The steps for creating a function are -

- Create a folder named **composables** in src and create a js file for the composable function
- Write the function and return the values you need to use in the component where you'll call this function
- Import the function in the vue file you want to use it in
- call the function and store data in variables

  ```js
  const { var1, var2, var3 } = functionName();
  return { var1, var2, var3 };
  ```

<a name="vuexStore"></a>

### Vuex Store

The vuex store is a centralized state management system for larger applications. The states of all the components are stored in here and it can be accessed from any component.

To setup vuex store -

- select Vuex option when creating the app. This creates a **store** folder in src with an **index.js** file.
- **state** - This is equivalent to the **data** option in a component where all the data is stored.

  ```js
  state: {
    elementName: 0,
  }
  ```

  To access a state element from a component -

  ```html
  <div>{{ $store.state.elementName }}</div>
  ```

- **mutations** - functions for changing the state are written here. We can not write asynchronus code here. Calling a function from mutation is known as commiting a mutation.

  ```js
  mutations: {
    functionName(state) {
      //change state property
    }
  }
  ```

  To commit a mutation from a component -

  ```html
  <button @click="$store.commit('function_name')">Button</button>
  ```

- **actions** - asynchronus code and code to call mutations functions is written here. It can access the state but can not change it directly. For changing the state, it needs to call a functions from mutations. Calling a function from actions is known as dispatching an action.

  ```js
    actions: {
      actionName() {
        //action body
      }
    }
  ```

  To dispatch an action from a component -

  ```html
  <button @click="$store.dispatch('action_name')">Button</button>
  ```

  **mutations functions should be called from actions, not directly from components. So there should always be two sets of the same function, one for mutations and another for actions.**

  To mutate the state using actions, we need to recieve a **commit** object as a parameter on the action. Then we can call a mutations function using commit and pass on the payload required to mutate the state. We also need to recieve the **payload** in the mutations function as a parameter along state.

  ```js
  mutations: {
    functionName(state, payload) {
      state.propertyName += payload
    }
  },
  actions: {
    actionName({ commit }) {
      axios("api_endpoint")
      .then(response => {
        commit('mutationsFunctionsName', payload)
      })
    }
  }
  ```

  An action can also recieve additional parameters other than commit.

  ```js
  actionName({ commit }, payload) {
    // action body
  }
  ```

- **getters** - getters are used for getting data from the state and modifying it before sending to a component, kind of like a computed property.
  To create a getter, we need to write a getter function that takes state as a parameter and returns a modified version of some property of the state.

  ```js
  getters: {
    getterName(state) {
      return state.property * 2;
    }
  }
  ```

- **modules** - this is used to divide the store into separate modules where each module has its own state, mutations and actions.

#### Vuex with text inputs and two way binding

For input, we have to bind the input with v-model to a computed property that includes a getter and setter. The getter gets the property value from the state while the setter dispatches an action for commiting a mutation to change the state.

```html
<input v-model="computedPropertyName" />
```

```js
computed: {
  computedPropertyName: {
    get() {
      return this.$store.state.propertyName
    },
    set(newValue) {
      this.$store.dispatch('actionName', newValue)
    }
  }
}
```
