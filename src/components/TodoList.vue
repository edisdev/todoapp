<template>
  <section class="TodoList-section">
    <div class="TodoList-section-title">
     <div class="actions">
      <div class="item">
      <button type="button"> <svg class="icon icon-list"><use xlink:href="#icon-list"></use></svg> </button>
      </div>
       <div class="item">
      <button type="button"> <svg class="icon icon-calendar"><use xlink:href="#icon-calendar"></use></svg> </button>
      </div>
     </div>
    </div>
    <div class="TodoList-section-content">
     <div class="list">
        <div class="list-item" v-for="item in list" :key="item.id" :class="{'maked' :item.maked}">
        <div class="item-icon">
         <button type="button"
                 @click="makedCheck(item.id)"></button>
        </div>
        <div class="item-maker">{{item.id}} - {{item.name}}</div>
        <div class="item-delete">
          <button type="button" @click="deleteItem(item.id)">
            <svg class="icon icon-cancel-circle"><use xlink:href="#icon-cancel-circle"></use></svg>
          </button>
        </div>
        </div>
    </div>
      <div class="new-item">
         <input type="text" name="new-item-value" v-model="newItem" placeholder="New Todo Item" @keyup.enter="addNewItem">
         <button type="button" @click.prevent="addNewItem"> + </button>
     </div>
     </div>
  </section>
</template>

<script>
export default {
  data() {
    return {
      list: [],
      newItem: null
    };
  },
  methods: {
    makedCheck(id) {
      this.list[id-1].maked = !this.list[id-1].maked;
    },
    addNewItem() {
      const index = this.list.length + 1;
      const newObj = {
        id: index,
        name: this.newItem,
        maked: false,
      };
      this.list.push(newObj);
      this.newItem = null;
    },
    deleteItem(id){
      const index = this.list.findIndex( item => item.id === id);
      this.list.splice(index,1);
    }
  }
};
</script>

<style lang="scss">
.icon {
  display: inline-block;
  width: 1em;
  height: 1em;
  stroke-width: 0;
  stroke: currentColor;
  fill: currentColor;
}
.TodoList-section {
  width: 400px;
  min-height: 600px;
  height: 100%;
  background-color: #fff;
  border-radius: 8px;
  position: relative;
  &-title {
    max-width: 400px;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    border-bottom: 1px solid rgba(#9b70c8, 0.5);
    .actions {
      min-height: 80px;
      display: flex;
      justify-content: space-between;
      width: 100%;
      .item {
        width: 50%;
        display: flex;
        align-items: center;
        &:first-child {
          justify-content: flex-start;
          border-right: 1px solid rgba(#9b70c8, 0.5);
          padding-left: 50px;
          button {
            color: #9b70c8;
          }
        }
        &:last-child {
          justify-content: flex-end;
          background-color: #fafafa;
          padding-right: 50px;
          border-top-right-radius: 8px;
          button {
            color: #c6c6c6;
          }
        }
      }
      button {
        background-color: transparent;
        font-size: 35px;
        cursor: pointer;
        padding: 0;
        border: none;
      }
    }
  }
  &-content {
    margin-top: 32px;
    overflow-y: auto;
    height: 418px;
    .list {
      padding-left: 20px;
      .list-item {
        color: #838383;
        font-size: 16px;
        display: flex;
        align-items: center;
        margin-bottom: 32px;
        position: relative;
        height: 40px;
        border-bottom: 1px solid rgba(#9b70c8, 0.2);
        .item-icon {
          width: 22px;
          height: 22px;
          margin-right: 15px;
          button {
            border: 2px solid #e9e9e9;
            border-radius: 7px;
            background: transparent;
            width: 100%;
            height: 100%;
            padding: 0;
            cursor: pointer;
            &:hover {
              border-color: #787878;
            }
          }
        }
        .item-maker {
          font-weight: 600;
        }
        .item-delete {
          position: absolute;
          right: 10px;
          display: none;
          button {
            font-size: 22px;
            cursor: pointer;
            color: rgba(#9b70c8, 0.5);
            border:none;
            background: transparent;
          }
        }
        &:hover {
         .item-delete  {
           display: block;
           button {
             color: #c6c6c6;
           }
         }
        }
        &.maked {
          .item-icon {
            button {
              &:after {
                display: flex;
                align-items: flex-end;
                font-weight: bold;
                content: "\2713";
                font-size: 27px;
                color: #9b70c8;
                transform: translateY(-13px);
              }
            }
          }
          .item-maker {
            text-decoration: line-through;
            opacity: 0.8;
          }
        }
      }
    }
    .new-item {
      position: absolute;
      bottom: 10px;
      width: 100%;
      padding-left: 10px;
      padding-right: 10px;
        width: calc(100% - 20px);
        display: flex;
        justify-content: space-between;
        input {
          width: 80%;
          height: 30px;
          border: 1px solid #9b70c8;
          border-radius: 4px;
          color: #9b70c8;
          padding: 7px;
          font-weight: bold;
          margin-right: 15px;
          &:focus {
            border: 2px solid #9b70c8;
          }
        }
        button {
          width: calc(20% - 15px);
          background-color: #9b70c8;
          color: #fff;
          border: none;
          font-size: 35px;
          border-radius: 4px;
          font-weight: bold;
        }
    }
  }
}
</style>
