<template>
  <div class="container-fluid">
    <div class="panel panel-primary">
      <div class="panel-heading">
        
      </div>
      <div class="panel-body form-inline">
        <label>
          電腦編號:
          <input type="text" class="form-control" v-model="id">
        </label>

        <label>
          姓名:
          <input type="text" class="form-control" v-model="name">
        </label>
        <label>
          分機號碼:
          <input type="text" class="form-control" v-model="ext">
        </label>

        <input type="button" value="新增" class="btn btn-primary text-white" @click='add'>
          <br>
          <br>
        <label>
          搜尋名字關鍵字：
          <input type="text" class="form-control" v-model="keywords">
        </label>
      </div>
    </div>
    <br>
    <br>
    <table class="table table-bordered table-hover table-striped">
      <thead>
        <tr>
          <th>電腦編號</th>
          <th>姓名</th>
          <th>分機</th>
          <th>刪除</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for='(item, key) in search(keywords)' :key='key'>
          <td>{{ item.id }}</td>
          <td>{{ item.name }}</td>
          <td>{{ item.ext }}</td>
          <td>
            <button type="button" class="closs ml-auto" @click='del(item)' aria-label="Close">
              <span aria-hidden="true">&times;</span>
            </button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script type="moudel">
import {ref} from 'vue';
export default {
  setup() {
    const id = ref('')
    const name= ref('')
    const ext =  ref('')
    const keywords = ref('')
    const list= ref ([
      { id: 1011, name: 'Claire', ext: '111' },
      { id: 1103, name: 'Eunice', ext: '222' },
      { id: 1220, name: 'Cliff', ext: '333' },
    ])

    const add = function() {
      
      var car = { id: this.id, name: this.name, ext: this.ext }
      this.list.push(car);
    }


    // 1. 參數為點擊的整筆資料 
    // 2. 使用forEach逐筆抓出vue data中的 list 的資料
    // 3. 比對點擊的該筆item和list中的哪筆資料id相同
    // 4. 刪除該筆資料 
    const del = function(list) {
      var newIndex = '';
      var vm = this;
      vm.list.forEach(function (item, key) {
        if (list.id === item.id) {
          newIndex = key;
        }
      })
      // .splice(索引值, 要刪除的筆數)
      this.list.splice(newIndex, 1);
    }

    const search = function(key) {
      var newList = [];
      this.list.forEach(item => {
        if (item.name.indexOf(key) != -1) {
          newList.push(item);
        }
      })
      return newList;
    }

    return {
      id, name, ext, list, keywords, add, del, search
    }
  }
}

  // data() {
  //   return{
  //   id: '',
  //   name: '',
  //   ext: '',
  //   keywords: '',
  //   list: [
  //     { id: 1011, name: 'Claire', ext: '111' },
  //     { id: 1103, name: 'Eunice', ext: '222' },
  //     { id: 1220, name: 'Cliff', ext: '333' },
  //   ]
  //   };
  // },
//   methods: {
//     add() {
//       var car = { id: this.id, name: this.name, ext: this.ext }
//       this.list.push(car);
//     },
//     // 1. 參數為點擊的整筆資料 
//     // 2. 使用forEach逐筆抓出vue data中的 list 的資料
//     // 3. 比對點擊的該筆item和list中的哪筆資料id相同
//     // 4. 刪除該筆資料 
//     del(list) {
//       var newIndex = '';
//       var vm = this;
//       vm.list.forEach(function (item, key) {
//         if (list.id === item.id) {
//           newIndex = key;
//         }
//       })
//       // .splice(索引值, 要刪除的筆數)
//       this.list.splice(newIndex, 1);
//     },
//     search(key) {
//       var newList = [];
//       this.list.forEach(item => {
//         if (item.name.indexOf(key) != -1) {
//           newList.push(item);
//         }
//       })
//       return newList;
//     }
//   }
// };


</script>

<style scoped></style>