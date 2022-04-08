<template>
  <div class="container">
    <div class="row g-1">
      <div class="col-12">
        <h3 class="text-primary fw-bold text-center my-3">
          Invoice Maker
          <a href="" target="_blank">
            <i class="fa-solid fa-file-circle-plus"></i>
          </a>
        </h3>
        <form action="" @submit.prevent="saveRecord">
          <div class="row">
            <div class="col-6">
              <select v-model="selectedProduct" class="form-select" required>
                <option
                  v-for="product in products"
                  :key="product.id"
                  :value="product.id"
                >
                  {{ product.name }} ({{ product.price }} MMK)
                </option>
              </select>
            </div>

            <div class="col">
              <input
                type="number"
                v-model="selectedQty"
                class="form-control"
                placeholder="Quantity"
                min="0"
                required
              />
            </div>

            <div class="col">
              <button class="btn btn-primary w-100">
                <i class="fa-solid fa-plus"></i>
              </button>
            </div>
          </div>
        </form>

        <table class="table table-striped mt-5">
          <thead>
            <tr>
              <th>-- # --</th>
              <th>Product</th>
              <th>Action</th>
              <th>Unit Price</th>
              <th>Quantity</th>
              <th>Cost</th>
            </tr>
          </thead>

          <tbody v-if="records.length">
            <tr v-for="(record, index) in records" :key="index">
              <td>
                <button
                  class="btn btn-danger btn-sm rounded-circle"
                  @click="del(index)"
                >
                  <i class="fa-solid fa-trash-can small"></i>
                </button>
              </td>
              <td>{{ record.product }}</td>
              <td>
                heello
              </td>
              <td>{{ record.price }}</td>
              <td>{{ record.qty }}</td>
              <td>{{ record.cost }}</td>
            </tr>
          </tbody>

          <tr v-else>
            <th colspan="6" class="text-center text-muted fs-4 py-4">
              No Record Yet!
            </th>
          </tr>

          <tfoot v-if="records.length">
            <tr>
              <td colspan="5">
                Total Cost
              </td>
              <td>{{ total }} Ks</td>
            </tr>
          </tfoot>
        </table>

        <div class="mt-5 text-center">
          <button class="btn btn-outline-success" @click="print">
            Print
          </button>

          <button class="btn btn-success ms-3 px-5" @click="save">Save</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      selectedProduct: '',
      selectedQty: '',
      products: [
        { id: 1, name: 'Apple', price: 500 },
        { id: 2, name: 'Tea Mix', price: 200 },
        { id: 3, name: 'Mevius', price: 2500 },
      ],
      records: [],
    }
  },

  methods: {
    saveRecord() {
      let currentProduct = this.products.find(
        (product) => product.id == this.selectedProduct,
      )

      let cost = currentProduct.price * this.selectedQty
      let record = {
        product: currentProduct.name,
        qty: this.selectedQty,
        price: currentProduct.price,
        cost,
      }
      this.records.push(record)
      this.selectedProduct = ''
      this.selectedQty = ''
    },

    del(index) {
      this.records.splice(index, 1)
    },

    print() {
      window.print()
    },

    save() {
      this.records = []
    },
  },

  computed: {
    total() {
      return this.records.reduce((acc, curr) => acc + curr.cost, 0)
    },
  },
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Lato:wght@100;300;400;700;900&family=Padauk:wght@400;700&display=swap');

$font-family-sans-serif: 'Lato', 'Padauk';

// @import '~bootstrap/scss/bootstrap.scss';
@import '~@fortawesome/fontawesome-free/css/all.css';
</style>
