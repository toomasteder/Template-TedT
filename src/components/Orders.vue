<template>
  <div>
    <h2 class="mb-3">Tellimused</h2>

    <b-table striped hover :items="items" :fields="fields">
      <template #cell(price)="data">
        <b class="text-info">{{ data.value }} EUR</b>
      </template>

      <template #cell(actions)="data">
        <b-button variant="success" @click="showProducts(data.item.products)"
          >Vaata tooteid</b-button
        >
      </template>
    </b-table>

    <!-- Toote tabel -->
    <!-- TODO: Add real data -->

    <b-modal id="modal-1" :title="productTableTitle" size="XL">
      <b-table striped hover :items="productItems" :fields="productFields">
      </b-table>
    </b-modal>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "Orders",
  data() {
    return {
      count: 0,
      fields: [
        "orderNumber",
        "orderDate",
        "status",
        { key: "price", label: "Hind" },
        "actions",
      ],
      items: [],
      productFields: [],
      productItems: [],
      productTableTitle: 'Pealkiri',
    };
  },
  async created() {
    const orders = await axios({
      url: "api/orders",
      method: "GET",
      headers: {},
    });
    console.log("orders", orders);
    // this.items = orders.data  //see esialgne ei lähe kokku meie osaga
    this.item = [
      {
        orderDate: "2021-01-31T09:28:58.250Z",
        _id: "601678abe3d51ab2cc5703d3",
        products: [
          {
            category: "CLOTHES",
            _id: "601678abe3d51ab2cc5703d4",
            name: "Valge pluus",
            productCode: "",
            price: 20,
            notes: "",
            amount: 1,
          },
        ],
        price: 20,
        status: "DONE",
        orderNumber: "TELLIMUS-1",
        __v: 0,
        id: "601678abe3d51ab2cc5703d3",
      },
      {
        orderDate: "2021-01-31T09:31:06.415Z",
        _id: "601678f79de1aeb314a93313",
        products: [
          {
            category: "CLOTHES",
            _id: "601678f79de1aeb314a93314",
            name: "Ilus valge pluus",
            productCode: "",
            price: 20,
            notes: "",
            amount: 1,
          },
        ],
        price: 20,
        status: "DONE",
        orderNumber: "TELLIMUS-2",
        __v: 0,
        id: "601678f79de1aeb314a93313",
      },
      {
        orderDate: "2021-01-31T11:04:14.415Z",
        _id: "60168f5968c486b5d8b1dca6",
        products: [
          {
            _id: "60168f5968c486b5d8b1dca7",
            name: "Ilus valge pluus",
            productCode: "123A123A123A1",
            category: "CLOTHES",
            price: 20,
            notes: "Kergesti määrduv",
            amount: 1,
          },
          {
            _id: "60168f5968c486b5d8b1dca8",
            name: "Kollane pluus",
            productCode: "123A123A123A4",
            category: "CLOTHES",
            price: 20,
            notes: "",
            amount: 2,
          },
        ],
        price: 60,
        status: "DONE",
        orderNumber: "TELLIMUS-3",
        __v: 0,
        id: "60168f5968c486b5d8b1dca6",
      },
    ];
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
