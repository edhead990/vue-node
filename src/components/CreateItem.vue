<template>
  <div>
    <h1>Create An Item</h1>
    <form v-on:submit.prevent="addItem">
      <div class="row">
        <div class="input-field col s6">
          <input type="text" id="item_name" v-model="item.name">
          <label for="item_name">Item Name:</label>
        </div>
      </div>
      <div class="row">
        <div class="input-field col s6">
          <input type="text" id="item_price" v-model="item.price">
          <label for="item_price">Item Price:</label>
        </div>
      </div>
      <button class="btn waves-effect waves-light">Add Item</button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      item: {}
    }
  },
  methods: {
    addItem() {
      let uri = 'http://localhost:4000/items/add';
      this.axios.post(uri, this.item).then(response => {
        this.$router.push({ name: "DisplayItem" });
      });
    }
  }
}
</script>