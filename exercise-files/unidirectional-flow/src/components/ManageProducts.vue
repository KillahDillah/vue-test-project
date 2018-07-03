<template>
  <section>
    <save-product-form
      :product="productInForm"
      v-on:submit="onFormSave"
      v-on:cancel="resetProductInForm"
    ></save-product-form>
    <product-list
      :products="products"
      v-on:edit="onEditClicked"
      v-on:remove="onRemoveClicked"
    ></product-list>
  </section>
</template>

<script>
import uuid from 'uuid'
import { mapGetters, mapActions } from 'vuex'
import ProductList from './ProductList'
import SaveProductForm from './SaveProductForm'

const initialData = () => {
  return {
    productInForm: {
      id: null,
      name: '',
      description: '',
      price: null
    },
    products: [
      {
        id: 'cc919e21-ae5b-5e1f-d023-c40ee669520c',
        name: 'COBOL 101 vintage',
        description: 'Learn COBOL with this vintage programming book',
        price: 399
      },
      {
        id: 'bcd755a6-9a19-94e1-0a5d-426c0303454f',
        name: 'Sharp C2719 curved TV',
        description: 'Watch TV like never before with the brand new curved screen technology',
        price: 1995
      },
      {
        id: '727026b7-7f2f-c5a0-ace9-cc227e686b8e',
        name: 'Remmington X mechanical keyboard',
        description: 'Excellent for gaming and typing, this Remmington X keyboard ' +
         'features tactile, clicky switches for speed and accuracy',
        price: 595
      }
    ]
  }
}

export default {
  components: {
    ProductList,
    SaveProductForm
  },
  computed: mapGetters({
  products: 'getProducts'
  }),
  data: initialData,
  methods: {
    ...mapActions([
      'saveProduct',
      'deleteProduct'
    ]),
    onFormSave (product) {
      this.saveProduct(product)

      this.resetProductInForm()
    },
    onEditClicked (product) {
      // since objects are passed by reference we need to clone the product
      // either by using Object.assign({}, product) or by using object
      // spread like we do here.
      this.productInForm = { ...product }
    },
    onRemoveClicked (productId) {
      this.deleteProduct(productId)

      if (productId === this.productInForm.id) {
        this.resetProductInForm()
      }
    }
  }
}
</script>
