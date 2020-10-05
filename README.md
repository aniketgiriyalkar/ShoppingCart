# ShoppingCart
Shopping Cart using Vue.js
- Aniket Giriyalkar (giriyalkar.aniket@gmail.com)


# Installations

- Official tool for building applications with Vue.js is Vue CLI. CLI stands for command line interface. Make sure node is installed before installing the Vue CLI. Then use the following command in the command line to install the CLI:
```np
npm install -g @vue/cli
```

- Then go into the project directory by doing a cd, for me its Desktop\Shopping Cart\ShoppingCart and type the following: 
```
vue create shopping-cart
```
shopping-cart is the name of the our project.

- We see an option of picking the default or manually select features. For manually selected features, we see features like Babel, TypeScript, Progressive Web App (PWA) Support, Router, Vuex, CSS Pre-Processors, Linter/ Formatter, Unit Testing and E2E Testing. We can turn these features on or off by pressing the Space key. Babel initially which allows us to write Javascript so that it works on older browsers and handles the transpiling of code into a more compatible version of JavaScript. TypeScript allows to work with types, progressive web app support gives the application bit of offline support and ability to work with different browsers and is a little better on mobile devices. Router allows us to navigate to different places within an application. Vuex is the sort of default way that Vue.js allows you to work with data sort of like a data model for view. CSS Pre-processors allow you to work with things like SAS or post RSS. Linter/ Formatter will install a few things that will mmake it easier to debug the code. Unit Testing and End to end(E2E) testing are different options of testing.

- I select Babel and Linter from these options. Next, I select the version 2.x of Vue.js to start the project with. ESLint + Prettier is the Linter / formatter config that is selected. Lint on save is selected as additional lint features. Package.json is selected for placing Babel, ESLint, etc. Use npm for downloading dependencies. This will begin installing CLI plugins. Once the installation is done, cd into the project directory(cd .\shopping-cart) and type the command
```
npm run serve
```
- This will start running the development version of the server and is going to process the project. App runs at http://localhost:8081 in the browser.
  
- Most of the things that we are going to be doing will be in the src folder. This is where everything is going to happen and hence it is the most important folder. The entry file for the application is going to be main.js. There is a components sub-folder where we put our sub components. An App.vue file is where the main components sit in. There is also an Assets folder which is where we put any images that the application needs in order to work.
- There is also a public folder that is for things that you don't really need to do anything in Vue.js with so you could put additional images here. There is an index.html file where you could put any HTML code here that is not going to be controlled by Vue.js. <div id="app"></div> is where the application is going to load, but everything else can be your code. If you were building this as a part of some other web page, you would just put in any scripts you want in here as well as any CSS. There's also a favicon which is an icon that loads up in your tabs on the browser. We can put anything else that we want in the public folder.

- We are almost never going to modify the main.js file. It is sort of like a loader that's going to bring in all the components that we need.
- In the App.vue file, the application is split into three seperate parts. One part will be a tempelate,and this is the same thing as when you create a component and you give that component a template attribute. Templates, subcomponents, any html has to be in a single div. It won't work when put in different divs. In addition, the file has a script section. This is where we put all the JavaScript. This will be equivalent of a script tag in regular index.html file. Component sections mentions the component that we are using, it should be located within the components sub folder. The third section is called style which is where we put any styles that we want to apply to a specific component. <style scoped> in HelloWorld.vue indicates that the style applies to this particular component only.

## Installing and importing additional modules
Animate.css bootstap jquery(bootstrap dependency) popper.js vue-outer are some modules we will be installing. This can be done in a single statement:
```
npm i --save animate.css bootstrap jquery popper.js vue-router
```
Next, we install a font library called font awesome: 
```
npm i --save @fortawesome/fontawesome-free @fortawesome/fontawesome-svg-core @fortawesome/free-solid-svg-icons @fortawesome/vue-fontawesome
```

- Next we get rid of all the unnecessary files that we won't be using. We remove the assets folder for now.

- In the main.js file, we import bootstrap and the bootstrap css folder manually. In the same way, we import the animated.css. Then import a library from svg icons.
```
import "bootstrap";
import { library } from "@fortawesome/fontawesome-svg-core";

import "bootstrap/dist/css/bootstrap.css";
import "animate.css/animate.css";

```

- The greyed out library import statement shows that we are importing a library from fortawesome but never using it. We import the Shopping Cart and Dollar Sign symbols from fort awesome library and add them to the library that we imported earlier.
```
import {
  faShoppingCart,
  faDollarSign
} from "@fortawesome/free-solid-svg-icons";

library.add(faShoppingCart, faDollarSign);
```

# Making sure our installations are working
- We will add some Bootstrap classes to see that Bootstrap is working properly. We add a container and a margin top of 5, which is done by 
```
  <div id="app" class="container mt-5">
```
- To check that the animation property is working, we use the following comand:
```
<p class="animate__animated animate__fadeInRight"> Take a look at our stock below</p>
```
- This will fade in the content from the right using animate.css library.

- Then, we import the fontawesome component using the <font-awesome-icon> tag, exactly like one would do a component in Vue.js. In here we are using the component that we installed while installing the Vue-Font Awesome version. The icon that we want is shopping-cart which was selected by going on the fontawesome website where the freely avaialable icons were explored. URL- https://fontawesome.com/icons?d=gallery&m=free
- The view-fontawesome documentation (https://github.com/fortawesomme/vue.fontawesome) was reffered to see how this library works and how to use these icons.

- We see that the modules we have imported are working properly 

# Working with Components
- In the components folder we create a Price.vue which will contain the Price component that we intend to create. This component adjusts every price in such a way that the Currency(prefix which is '$' by default) is denoted before the price which is formatted(by default upto 2 digits after decimal) and the conversion is properly evaluated using a conversion factor(by default 1). Here is what the code looks like for this component.

```
Price.vue

<template>
    <span>{{ this.prefix + Number.parseFloat(this.value * this.conversion).toFixed(this.precision) }}</span>
</template>

<script>
export default {
    props: {
        value: Number, 
        prefix: {
            type: String,
            default: '$'
        },
        precision: {
            type: Number,
            default: 2
        },
        conversion: {
            type: Number,
            default: 1
        } 
    }   
}
</script>
```

- Next we have to import this into App.vue which is done by importing the component in that file. <price value="10.99"></price> is added inside the div to check if it is working correctly. Here is the updated App.vue file looks like:
```
App.vue

  
<template>
    <div id="app" class="container mt-5">
        <h1>My Shop</h1>
        <p class="animate__animated animate__fadeInRight">Take a look at our offerings below</p>
        <font-awesome-icon icon="shopping-cart"></font-awesome-icon>
        <price value="10.99"></price>
    </div>
</template>

<script>
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";
import Price from './components/Price.vue'

export default {
  name: "app",
  components: {
    FontAwesomeIcon,
    Price
  }
};
</script>
```

- Once we make the above changes, we should be able to see the price info correctly. In our case we see "$10.99" beside the shopping cart icon.

- Next, we move on to the Product List component. We create a new file ProductsList.vue in the components subdirectory. We create a skeleton by adding the <template></template> and <script></script> sections.

- The name of this component will be product-list. We will import the Price component from the components directory and include that in the components section. We have the props sections that consists of "products" and "maximum" which are passed from the main component. We also have a methods section that consists of methods like beforeEnter: that shows the view before any items enter the window. enter: tnat shows the state of window when the products enter, and leave: which consists of the functionality while the item is supposed to leave the window.
- In the App.vue we remove the <p></p> tag and other components that we used to test our imports and now add the <products-list :maximum="maximum" :products="products"> components that will require maximum value and array of productes to be passed as props. We add that in the data: section in export default section of the App.vue file. This data will be a function and will return an object that we want. We define maximum as 99 and products as null for right now.
- To get the products information we will be bringing in a lifecycle method under mounted. This will fetch the products information from the URL "https://hplussport.com/api/products/order/price" and store it as the products information. This brings in the data from the API and needs to be done in the parent component(App.vue) and can be passed onto the child components as props.
- Now, we will no longer require the Price component to be called from App.vue as we are already calling it within the ProductsList Component. We remove that from App.vue and import the ProductList in the components. The updated App.vue file looks like:
```
App.vue

<template>
  <div id="app" class="container mt-5">
    <h1>My Shop</h1>
    <product-list :maximum="maximum" :products="products"></product-list>
  </div>
</template>

<script>
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";
import ProductList from "./components/ProductList.vue";

export default {
  name: "app",
  data: function() {
    return {
      maximum: 99,
      products: null
    };
  },
  components: {
    FontAwesomeIcon,
    ProductList
  },
  mounted: function() {
    fetch("https://hplussport.com/api/products/order/price")
      .then(response => response.json())
      .then(data => {
        this.products = data;
      });
  }
};
</script>
```

- The following is the code for the ProductList component that we created:
```
ProductList.vue

<template>
  <div id="app" class="container mt-5">
    <h1>My Shop</h1>
    <product-list :maximum="maximum" :products="products"></product-list>
  </div>
</template>

<script>
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";
import ProductList from "./components/ProductList.vue";

export default {
  name: "app",
  data: function() {
    return {
      maximum: 99,
      products: null
    };
  },
  components: {
    FontAwesomeIcon,
    ProductList
  },
  mounted: function() {
    fetch("https://hplussport.com/api/products/order/price")
      .then(response => response.json())
      .then(data => {
        this.products = data;
      });
  }
};
</script>

```
- Now when we type the "npm run serve command" we can see that the Products show up on the application.

## Using Chrome DevTools
- We download the Vue.js devtools to look at what's happening with the Vue application. After installing it, when we inspect the element, we see an extra tab called Vue that shows up. It will help us in understanding whats happening with the application and all the different components that we have available and what is happening in each of those components.

- Right now the + buttons should emit an event that should add an item in the cart but it is not wired up yet. When we click on the button, we are emitting an event called add which passes along the information of the item that is being clicked on.

- As of now we are not catching the item that is being added, in the App.vue where we use the product-list component we notice that we are not capturing that event. To make sure we do that we add the "@add-"addItem"" inside of our product-list component. AddItem is a trigger which needs to be configured into the component.

- The updates made in the App.vue file are as follows:
```
<product-list :maximum="maximum" :products="products" @add="addItem">
    </product-list>

export default {
  name: "app",
  data: function() {
    return {
      maximum: 99,
      cart: [],
      products: null
    };
  },
  methods: {
    addItem: function(product) {
      var whichProduct;
      var existing = this.cart.filter(function(item, index) {
        if (item.product.id == Number(product.id)) {
          whichProduct = index;
          return true;
        } else {
          return false;
        }
      });
      if (existing.length) {
        this.cart[whichProduct].qty++;
      } else {
        this.cart.push({ product: product, qty: 1 });
      }
    }
  },
  components: {
    FontAwesomeIcon,
    ProductList
  },
  mounted: function() {
    fetch("https://hplussport.com/api/products/order/price")
      .then(response => response.json())
      .then(data => {
        this.products = data;
      });
  }
};
```

- Now, whenever we click on a add button, we can see in the Vue section of the inspect element that the data of app is updated on every click and the product information, and quantity is stored.

- Hence this extension gives us a way of tracking what is exactly going on with the application. When we click on an event, it shows things like event type and payload which is the things that are being passed along through the application to the methods. This will make the ability to program things a lot more easier.


# Building a Slider
- Let's now build a slider that allows us to qualify these items based on their price. For this we create a component called PriceSlider.vue, which is going to have <template></template> and <script></script> tags. For this component we will also have <style></style> tag.
- The slider styling and sizing is defined by the transition tag which is written in the template. In here we define the styling and sizing for slider.
- In the script tag we give the name "price-slider". The ":class="sliderState"" determines whether or not the slider is going to show or not. In the computed section we have a sliderState function that makes the status d-flex or d-none. This is something that we will pass from the parent component as a prop.
- Then we wire it up with the parent component by making changes in the App.vue file. We import the PriceSlider component. We call the component price-slider and specify the slider-status and add that variable in data. We initialize it with a value true so that the slider shows.
- We see that the input box is too wide, we arrange that styling in the PriceSlider.vue. We see that the slider is still not working for the value that we type in the input box. we see that the maximum field is not getting the value from the parent component, it is not updating that particular value. We could do it by passing along events from parent component. To avoid the conflict of parent modifying this variable, we have an value inside this component to keep track of the value and then communicate  with the parent component and allow it to modify the maximum variable as it wants to.
- Inside PriceSlider.vue, we create a varible called maxAmount and set it to 70. Now, instead of keeping a track of maximum in vmodel, we will keep track of maxAmount. Range will modify this maxAmount variable. Now we need to communicate with the parent that we are modifying it.
- To do that, we need to emit the change in value everytime it occurs @change="$emit('update:maximum', maxAmount)". In the range the event is going to be @input="$emit('update:maximum', maxAmount)".
- Now we go into the parent component and communicate that. We sync the maximum value with what we get from the event. Whenever it changes it's going to trigger an event and push it up in a parent and that event is going to sync with value of maximum coming from the sub-component inside the component using :maximum.sync="maximum". We see that the slider works perfectly fine now.
-  We add some final styling and animation functionality to the slider.
```
ProductSlider.vue

<template>
  <transition name="fade">
    <div v-if="sliderStatus">
      <div class="align-items-center" :class="sliderState">
        <label class="font-weight-bold mr-2" for="formMax">max</label>
        <input
          type="text"
          id="formMax"
          class="form-control mx-2 test-center"
          style="width: 60px;"
          v-model="maxAmount"
          @change="$emit('update:maximum', maxAmount)"
        />
        <input
          type="range"
          class="custom-range"
          min="0"
          max="200"
          v-model="maxAmount"
          @input="$emit('update:maximum', maxAmount)"
        />
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  name: "price-slider",
  data: function() {
    return {
      maxAmount: 70
    };
  },
  props: ["sliderStatus"],
  computed: {
    sliderState: function() {
      return this.sliderStatus ? "d-flex" : "d-none";
    }
  }
};
</script>
<style>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
}
</style>

```

- Updates in the App.vue file:
```
App.vue

<template>
  <div id="app" class="container mt-5">
    <h1>My Shop</h1>
    <price-slider :sliderStatus="sliderStatus" :maximum.sync="maximum">
    </price-slider>
    <product-list :maximum="maximum" :products="products" @add="addItem">
    </product-list>
  </div>
</template>

<script>
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";
import ProductList from "./components/ProductList.vue";
import PriceSlider from "./components/PriceSlider.vue";

export default {
  name: "app",
  data: function() {
    return {
      maximum: 70,
      sliderStatus: true,
      cart: [],
      products: null
    };
  },
  methods: {
    addItem: function(product) {
      var whichProduct;
      var existing = this.cart.filter(function(item, index) {
        if (item.product.id == Number(product.id)) {
          whichProduct = index;
          return true;
        } else {
          return false;
        }
      });
      if (existing.length) {
        this.cart[whichProduct].qty++;
      } else {
        this.cart.push({ product: product, qty: 1 });
      }
    }
  },
  components: {
    FontAwesomeIcon,
    ProductList,
    PriceSlider
  },
  mounted: function() {
    fetch("https://hplussport.com/api/products/order/price")
      .then(response => response.json())
      .then(data => {
        this.products = data;
      });
  }
};
</script>

```
# Adding Navigation and Cart
- Now we create a component called Navbar.vue. We call this component "navbar". As Props for this component we have cart, cartQty and cartTotal. We import the components Price and FontAwesomeIcon for displaying the price and remove icons.
- In the App.vue, we add the navbar component above price-slider and in that we pass the information cart, cartQty and cartTotal.
```
<navbar
      :cart="cart"
      :cartQty="cartQty"
      :cartTotal="cartTotal"
    ></navbar>
```
- Then we import the component and add it in the components section. To make sure the component is working, we need to modify the state of the slider that exisits in the parent component. We handle this by emiting the toggle and in the parent component we will need to catch that. So toggle will execute a local method called toggleSliderStatus.
- We see that the Total price is not showing up in the cart and the remove item button is not yet working. Let's fix that. We add the deleteItem function in the methods section of App.vue file:
```
deleteItem: function(id) {
      if (this.cart[id].qty > 1) {
        this.cart[id].qty--;
      } else {
        this.cart.splice(id, 1);
      }
    },
```
- We also need to define the computed properties cartTotal and cartQty:
```
  cartTotal: function() {
    let sum = 0;
    for (key in this.cart) {
      sum = sum + this.cart[key].product.price * this.cart[key].qty;
    }
    return sum;
  },
  cartQty: function() {
    let qty = 0;
    for (key in this.cart) {
      qty = qty + this.cart[key].qty;
    }
    return qty;
  }
```
- Now, we see that the numbers $0.00 show up which still not correct nut is an inprovement to NaN. While we add these items we are facing some issues which we are not yet aware of. We do the inspect element to study what the problem is in the console. It says that the key isn't defined, so I add the let keyword before the key variable in the for loops. This fixes the total value of the cart which now shows up the card total and price accurately.

- Now moving on to wiring up the deleting functionality. We inspect the problem and observe that deleteItem isn't a function, which means something to do with the button click event in the navbar component. The deleteItem component exists in the parent and is not accessible inside the navbar.vue. So, here we need to emit so that we go back up the chain.
```
  @click.stop="$emit('delete', index)"

```

- We ensure that the stop modifier is there to prevent the bootstrap dropdown from going back up. Make sure we capture this in the App.vue file. In the navbar we add a @delete event and send that to the deleteItem method that we defined.

```
Navbar.vue
<template>
  <nav class="navbar navbar-light fixed-top">
    <div class="navbar-text ml-auto d-flex">
      <button class="btn btn-sm btn-outline-success" @click="$emit('toggle')">
        <i class="fas fa-dollar-sign"></i>
        <font-awesome-icon icon="dollar-sign"></font-awesome-icon>
      </button>
      <div class="dropdown ml-2" v-if="cart.length > 0">
        <button
          class="btn btn-success btn-sm dropdown-toggle"
          id="cartDropdown"
          data-toggle="dropdown"
          aria-haspopup="true"
          aria-expanded="false"
        >
          <span class="badge badge-pill badge-light">{{ cartQty }}</span>
          <i class="fas fa-shopping-cart mx-2"></i>
          <price :value="Number(cartTotal)"></price>
        </button>
        <div
          class="dropdown-menu dropdown-menu-right"
          aria-labelledby="cartDropdown"
        >
          <div v-for="(item, index) in cart" :key="index">
            <div class="dropdown-item-text text-nowrap text-right">
              <span class="badge badge-pill badge-warning align-text-top mr-1">
                {{ item.qty }}
              </span>
              {{ item.product.name }}
              <b>
                <price :value="Number(item.qty * item.product.price)"></price>
              </b>
              <a
                href="#"
                @click.stop="$emit('delete', index)"
                class="badge badge-danger text-white"
                >-
              </a>
            </div>
          </div>
        </div>
      </div>
    </div>
  </nav>
</template>

<script>
import Price from "./Price.vue";
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";

export default {
  name: "navbar",
  props: ["cart", "cartQty", "cartTotal"],
  components: {
    FontAwesomeIcon,
    Price
  }
};
</script>

```

- We see that the toggle button, add item, delete item, cart total, cart quatity, item quantity and transisitons are working perfectly fine.

# Using Vue Router
- Allows us to create something equivalent to pages on our application. We plan to create a checkout page and for that we need to move PriceSlider, ProductList and Navbar components from App.vue into a sub component of sorts. 
- We create a Products.vue component and have the template and script tags included. Within the template inside a container div we add our components. We cut these subcomponents from App.vue and paste them in the Products.vue which is going to load the other subcomponents. In the script, we will import these components. Name this component as products, include all the props that would be required by our components. We also import the components in the components section.
```
<template>
  <div>
    <h1>Shopping Cart Project</h1>
    <navbar
      :cart="cart"
      :cartQty="cartQty"
      :cartTotal="cartTotal"
      @toggle="toggleSliderStatus"
      @delete="deleteItem"
    ></navbar>
    <price-slider :sliderStatus="sliderStatus" :maximum.sync="maximum">
    </price-slider>
    <product-list :maximum="maximum" :products="products" @add="addItem">
    </product-list>
  </div>
    
</template>
<script>
import Navbar from './Navbar.vue';
import ProductList from "./components/ProductList.vue";
import PriceSlider from "./components/PriceSlider.vue";

export default {
  name: 'products',
  props: [
    "products",
    "maximum",
    "cart",
    "cartQty",
    "cartTotal",
    "sliderStatus",
    "sliderState"
  ], 
  components: {
    Navbar,
    PriceSlider,
    ProductList
  }
    
}
</script>
```
- Now in the App.vue, we need to import the Products.vue component. The product is going to be the loader that loads the other things. We will need to connect App.vue to it. We will call the <products></products> and pass all the parameters here.

- We see that the components show up properly on, however the events are not yet wired up. To connect the events, we will have to look at all the emit statements and add $parent. before all the events that we emitted. Again all the funcitonality works as it is expected to. We have brought everything down a level.

```
Products.vue

<template>
  <div>
    <h1>Shopping Cart Project</h1>
    <navbar
      :cart="cart"
      :cartQty="cartQty"
      :cartTotal="cartTotal"
      @toggle="toggleSliderStatus"
      @delete="deleteItem"
    ></navbar>
    <price-slider :sliderStatus="sliderStatus" :maximum.sync="maximum">
    </price-slider>
    <product-list :maximum="maximum" :products="products" @add="addItem">
    </product-list>
  </div>
</template>
<script>
import Navbar from "./Navbar.vue";
import ProductList from "./ProductList.vue";
import PriceSlider from "./PriceSlider.vue";

export default {
  name: "products",
  props: [
    "products",
    "maximum",
    "cart",
    "cartQty",
    "cartTotal",
    "sliderStatus",
    "sliderState"
  ],
  components: {
    Navbar,
    PriceSlider,
    ProductList
  }
};
</script>
```

## Building a Checkout Page

- Next we will be building a component that will have the checkout information. We create a new component called Checkout.vue. We name this component checkout and cart and cartTotal are the props that we will need. Proce is the component we import. We create a basic layout table of the checkout page using bootstrap classes and in this we add v-if statement to make sure that it will only show up if the cart has a certain length. Otherwise it won't show up.
- For the total, we will be using a price component, and use the value as cart total. Then we will need to go to the tr which will be repeating over and over, this will require a v-for statement. It will ask for rthe item, index and the cart. We will add the key as item.product.id.
- In our buttons, we need to emit the respective events. For add button its going to emit add and pass along the item that I want to add. It will quickly allow us to add the additional copies of the product if we want to. The other button will the delete button and it will be similar. We will be passing along the index as that is all we will be needing to delete an item.
- For populating the information, we add the following snippet 
```
  <th scope="row">{{ item.product.name }}</th>
  <td class="text-center">{{ item.qty }}</td>
  <td class="text-right">{{ Number(item.product.price) }}</td>
  <td class="text-right">{{ Number(item.qty * item.product.price) }}</td>
```

- Next, we need to bring this component into the main component. For now we will just put it at the top of Products in App.vue. We will pass the required parameters to this new component. We will also have to import and register this component.

- Once we wire up this component we can see that the items that we have selected appear in the checkout just above. We see that the button events are emit events, we change that to click events.

```
Checkout.vue

<template>
  <div>
    <h1>Checkout</h1>

    <table class="table table-hover" v-if="cart.length">
      <caption class="text-right h3">
        <b>Total:</b>
        <price
          class="d-block text-success font-weight-light"
          :value="Number(cartTotal)"
        >
        </price>
      </caption>
      <thead>
        <tr>
          <th scope="col"></th>
          <th scope="col">Item</th>
          <th scope="col" class="text-center">Qty</th>
          <th scope="col" class="text-right">Price</th>
          <th scope="col" class="text-right">Sub-total</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, index) in cart" :key="item.product.id">
          <td class="text-center">
            <div class="btn-group" role="group" aria-label="Basic example">
              <button @click="$emit('add', item.product)" class="btn btn-info">
                +
              </button>
              <button
                @click="$emit('delete', index)"
                class="btn btn-outline-info"
              >
                -
              </button>
            </div>
          </td>
          <th scope="row">{{ item.product.name }}</th>
          <td class="text-center">{{ item.qty }}</td>
          <td class="text-right">{{ Number(item.product.price) }}</td>
          <td class="text-right">
            {{ Number(item.qty * item.product.price) }}
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import Price from "./Price.vue";

export default {
  name: "checkout",
  props: ["cart", "cartTotal"],
  components: {
    Price
  }
};
</script>
```
- Next we move these into two seperate pages. But before that we observe several errors in the console for methods that aren't really being used. To get rid of these errors all that we need to do is get rid of the paramenters in Product.vue that call methods as $parent.$emit emit those events into the App.vue. Now we do not see any errors in the console.

- In the main.js, we import VueRouter from the vue-router library. To configure the Vue router we write the statement Vue.use(VueRouter). Now to setup a the URL's, we have to set up the route which is done by the following statements:
```
main.js

import Vue from "vue";
import VueRouter from "vue-router";
import App from "./App.vue";
import "bootstrap";
import { library } from "@fortawesome/fontawesome-svg-core";

import "bootstrap/dist/css/bootstrap.css";
import "animate.css/animate.css";

import {
  faShoppingCart,
  faDollarSign
} from "@fortawesome/free-solid-svg-icons";

library.add(faShoppingCart, faDollarSign);

import Products from "./components/Products.vue";
import Checkout from "./components/Checkout.vue";
Vue.use(VueRouter);
Vue.config.productionTip = false;

const router = new VueRouter({
  routes: [
    {
      path: "*",
      component: Products
    },
    {
      path: "/checkout",
      component: Checkout
    }
  ]
});

new Vue({
  render: h => h(App),
  router
}).$mount("#app");

```
- Once we have created different routes(one route  and the default) and imported the components that are goint to fit into those routes. We need to get them on the page. To do that we go into the App.vue and instead of importing two different pages, we import a single thing called router-view. To this we are going to pass all that we would normally pass to both the pages.

- When we run the application, we see that the items that we have added to the cart can be observed in the checkout page localhost:8081/checkout. We see that everything is working fine. Next, we move on to creating links to navigate to and from the home page into the checkout page.  

- To do that in the Checkout.vue, we add a <router-link> with bootstrap classes for styling and a to directive that specifies where the link is supposed to go to.
```
  <router-link class="btn btn-sm btn-outline-info text-dark" to="/">
    Continue Shopping
  </router-link>
```

- Next, we have to create a link from home page to the checkout page. We use a similar code in the Nav bar.