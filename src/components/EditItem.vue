<template>
  <div>
    <h1>Update Item</h1>
    <div class="row">
      <div class="col s12"><router-link :to="{ name: 'DisplayItem' }" class="btn btn-success">Return to Items</router-link></div>
    </div>

    <form v-on:submit.prevent="updateItem">
      <div class="input-group">
        <label>Item Name</label>
        <input type="text" v-model="item.name">
      </div>

      <div class="input-group">
        <label name="product_price">Item Price</label>
        <input type="text" v-model="item.price">
      </div>

      <button class="btn waves-effect waves-light">Update</button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      item: {}
    };
  },

  created: function() {
    this.getItem();
  },

  methods: {
    getItem() {
      let uri = "http://localhost:4000/items/edit/" + this.$route.params.id;
      this.axios.get(uri).then(response => {
        this.item = response.data;
      });
    },

    updateItem() {
      let uri = "http://localhost:4000/items/update/" + this.$route.params.id;
      this.axios.post(uri, this.item).then(response => {
        this.$router.push({ name: "DisplayItem" });
      });
    }
  }
};
</script>