<template>
  <div>
    <h1>Items</h1>

    <div class="row">
      <div class="col s2">
        <router-link :to="{ name: 'CreateItem' }" class="btn waves-effect waves-light">Create Item</router-link>
      </div>
    </div>

    <table class="highlight">
      <thead>
        <tr>
          <td>ID</td>
          <td>Item Name</td>
          <td>Item Price</td>
          <td>Actions</td>
        </tr>
      </thead>

      <tbody>
        <tr v-for="(item, key, index) in items" :key="key">
          <td>{{ item._id }}</td>
          <td>{{ item.name }}</td>
          <td>{{ item.price }}</td>
          <td>
            <router-link :to="{name: 'EditItem', params: { id: item._id }}" class="btn waves-effect waves-light">Edit</router-link>
            <button class="btn red waves-effect waves-light" v-on:click="deleteItem(item._id)">Delete</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      items: []
    };
  },

  created: function() {
    this.fetchItems();
  },

  methods: {
    fetchItems() {
      let uri = "http://localhost:4000/items";
      this.axios.get(uri).then(response => {
        this.items = response.data;
      });
    },
    deleteItem(id) {
      let uri = 'http://localhost:4000/items/delete/'+id;
      this.items.splice(id, 1);
      this.axios.get(uri);
    }
  }
};
</script>