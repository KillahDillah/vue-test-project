<template>
  <!-- when using a component in a template Vue.js expects the DOM element to be
  lowercased and dasherized. e.g. ProductList -> product-list -->

  <manage-products></manage-products>
  
</template>

<script>
import ManageProducts from './components/ManageProducts'
import ProductList from './components/ProductList'
import SaveProductForm from './components/SaveProductForm'

export default {
  components: {
    // With ES6 we can use the Object Literal Shorthand Syntax to save us some
    // keystrokes
    ProductList,
    SaveProductForm,
    ManageProducts
  }
}
</script>