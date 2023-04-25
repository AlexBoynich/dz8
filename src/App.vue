<template>
  <div class="section">
    <ol class="table" multiple>
      <li v-for="(item, index) in itemListLeft"
      :class="{selectedLi:  item.selected }"
      @click="doSelected(item)"
      :key="index"
       >
        {{ item.text }}
      </li>
    </ol>
    <div class="images">
      <img
      @click="runObjLeft(itemListLeft, itemListRight)"
      src="../public/arrow.png" alt="">
      <img
      @click="runObjRight(itemListLeft, itemListRight)"
      class="img2" src="../public/arrow.png" alt="">
    </div>
    <ol class="table">
      <li v-for="(itemRight, index) in itemListRight"
      :class="{selectedLi: itemRight.selected}"
      @click="doSelected(itemRight)"
      :key="index"
      >
        {{ itemRight.text }}
      </li> 
    </ol>
  </div>
</template>

<script>

  export default {
    data () {
      return {
        itemListLeft: [
          {text: 'first-item', id: 0, selected: false},
          {text: 'second-item', id: 1, selected: false},
          {text: 'third-item', id: 2, selected: false},
          {text: 'fourth-item', id: 3, selected: false},
          {text: 'fifth-item', id: 4, selected: false},
        ],
        itemListRight: [
        {text:'alone-item', id: 5, selected: false}
        ],
      }
    },
    methods: {
      doSelected (item) {
        item.selected = !item.selected;
      }, 
      runObjRight(itemListLeft, itemListRight) {
        let selectedItems = itemListLeft.filter((item) => item.selected === true);
        this.itemListLeft = itemListLeft.filter((item) => item.selected === false);
        this.itemListRight = [...itemListRight, ...selectedItems];
        for(let item of itemListLeft) {
          item.selected = false;
        }
        for(let item of itemListRight) {
          item.selected = false;
        }
        console.log(selectedItems, itemListRight)
          },
      runObjLeft(itemListLeft, itemListRight) {
        let selectedItems = itemListRight.filter((item) => item.selected === true);
        this.itemListRight = itemListRight.filter((item) => item.selected === false);
        this.itemListLeft = [...itemListLeft, ...selectedItems]
        for(let item of itemListLeft) {
          item.selected = false
        }
        for(let item of itemListRight) {
          item.selected = false;
        }
        console.log(selectedItems, itemListRight)
          }
          
      },
      cloneObj(itemList, index) {
        let newObj= {};
        Object.assign(newObj, itemListLeft[index])
        return newObj;
      },
      deleteObj(itemList, index) {
        itemList.splice(index, 1)
      },
      pushObj(itemList, obj) {
        itemList.push(obj)
      },
    };



</script>

<style>
  .section {
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .table {
    display:flex;
    border: 1px solid gray;
    flex-direction: column;
    justify-content: flex-start;
    padding: 30px;
    min-width: 400px;
    min-height: 400px;
  }
  li{
    list-style-type: none;
    margin: 20px;
  }
  li:hover{
    cursor: pointer;
  }
  .selectedLi{
    background-color: rgb(0, 162, 255);
  }
  img{
    width: 50px;
    height: 50px;
    margin: 20px;
  }
  img:hover {
    cursor: pointer;
  }
  .img2{
    rotate: 180deg;
  }
  .images {
    display: flex;
  }
</style>
