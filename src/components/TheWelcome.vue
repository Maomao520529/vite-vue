<template>
  <div class="home">
    <div class="text-end">
      <button type="button"
      @click="addItem"
      class="btn btn-success mt-3">新增</button>
    </div>
    <table class="table table-striped  table-hover mt-3">
      <thead class="table-dark">
      <tr class="text-center">
        <th>No.</th>
        <th>標題</th>
        <th>圖片</th>
        <th width="100">銷售狀態</th>
        <th>編輯</th>
        <th>刪除</th>
      </tr>
    </thead>
    <tbody>
      <tr class="text-center align-middle"
          v-for="(itemTable, key) in data" :key="itemTable.id"
           :class="{'table-success': itemTable.onStock}">
        <td>{{ key + 1 }}</td>
        <td>{{ itemTable.title}}</td>
        <td> <img :src="itemTable.thumbnailUrl" alt="" height="100"></td>
        <td><input type="checkbox" v-model=" itemTable.onStock">
        </td>
        <td>
          <button type="button" class="btn btn-outline-success"
              @click="editItem(itemTable)">修改</button>
        </td>
        <td>
          <button type="button" class="btn btn-outline-danger"
           @click="deleteItem(itemTable)">X</button>
        </td>
      </tr>
    </tbody>
    </table>
    <div>
       <form v-if="isNew || temp.id">
      <div class="mb-3">
        <label :for="productName" class="form-label text-black">產品名稱</label>
        <input type="text" :id="productName" class="form-control"
        v-model="temp.title">
      </div>
      <div class="mb-3">
        <img :src="temp.thumbnailUrl" class="img-fluid d-block" alt="" width="300">
        <label :for="productImage"
        class="form-label text-black">產品圖片</label>
        <input type="text" :id="productImage"
          class="form-control"
          v-model="temp.thumbnailUrl"
        >
      </div>
      <button type="button"
       class="btn btn-success"
        v-on:click="confirmEdit">更新</button>
    </form>
  </div>
   
  </div>
</template>

<script>
export default {
  data() {
    return {
      data: [],
      temp: {},
      cacheArea: '',
      isNew: false,
      onStock: false
    }
  },
  mounted() {
     const apiUrl = 'https://jsonplaceholder.typicode.com/photos';

      this.$http.get(apiUrl)
      .then((res) => {
        // 取得遠端資料
        this.data = res.data.slice(0,5).sort(() => 0.5 - Math.random());
        console.log(this.data); 
      })
      .catch(err => {
        console.log(err.response);
      })
    },
    methods: {
      addItem() {
        this.isNew = true;
        this.temp = {};
      },
      editItem(item) {
        this.temp = {...item};
      },
      deleteItem(item) {
        this.data.splice(this.data.indexOf(item), 1);
      },
      confirmEdit() {
        if (!this.temp.id) {
          this.temp.id = new Date().getTime();
          this.temp.onStock = false;
          this.data.push(this.temp);
          this.temp = {};
        }else {
          this.data.forEach((item, i) => {
            if (item.id === this.temp.id) {
              this.data[i] = this.temp;
            }
          });
        }
        this.isNew = false;
        this.temp = {};
      }
    },
  }
</script>