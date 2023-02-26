<template>
  <div class="select">
    <div  class="select__top top">Туристы</div>
    <div class="select__input input"
      @click="this.isSelectOpened = !this.isSelectOpened"
      :class="{ _active: isSelectOpened }"> {{adult}} взрослых
    </div>

    <div 
      v-if="isSelectOpened"
      class="select__body">

      <div class="select__adult"> 
        <span 
        @click="incr"
        class="select__adult-btn">
          <svg width="16" height="16" viewBox="0 0 16 16" fill="none" xmlns="http://www.w3.org/2000/svg">
          <path fill-rule="evenodd" clip-rule="evenodd" d="M1.00012 8.00024C1.00012 7.44796 1.44784 7.00024 2.00012 7.00024L14.0001 7.00025C14.5524 7.00025 15.0001 7.44796 15.0001 8.00025C15.0001 8.55253 14.5524 9.00025 14.0001 9.00025L2.00012 9.00024C1.44784 9.00024 1.00012 8.55253 1.00012 8.00024Z" fill="#1B2640"/>
          </svg>
        </span>   
        <span class="select__adult-content"> {{adult}} взрослых </span>   
        <span @click="decr"
        class="select__adult-btn">
          <svg width="16" height="16" viewBox="0 0 16 16" fill="none" xmlns="http://www.w3.org/2000/svg">
          <path fill-rule="evenodd" clip-rule="evenodd" d="M9.00004 2C9.00004 1.44772 8.55233 1 8.00004 1C7.44776 1 7.00004 1.44771 7.00004 2L7.00004 7.00016L2.00024 7.00016C1.44796 7.00016 1.00024 7.44788 1.00024 8.00016C1.00024 8.55245 1.44796 9.00016 2.00024 9.00016L7.00004 9.00016L7.00004 14C7.00004 14.5523 7.44775 15 8.00004 15C8.55232 15 9.00004 14.5523 9.00004 14L9.00004 9.00016L14.0002 9.00016C14.5525 9.00016 15.0002 8.55245 15.0002 8.00016C15.0002 7.44788 14.5525 7.00016 14.0002 7.00016L9.00004 7.00016L9.00004 2Z" fill="#1B2640"/>
          </svg>
        </span> 
      </div>

      <ul class="select__children-list">
          <div class="select__children-item"
          v-for="child, i in children"
          :key=i>
          выбран ребенок {{ child }}
        </div>
        </ul>

      <div  class="select__children input"
      @click= "toggleChildrenOpened">
        Добавить ребенка

        <ul class="select__age"
        v-if="isChildrenOpened">
          <li
          v-for="option, i in opt"
          @click="pushChild(option)"
          :key=i
          > {{ option }}</li>
        </ul>
      </div>

    </div>

  </div>
</template>

<script>
export default {
  data() {
    return {
      adult: 2,
      opt: ['Меньше 2 лет', '2','3','4','5','6','7','8','9','10','11'],
      children: [],
      isSelectOpened: true,
      isChildrenOpened: true,
    }
  },

  methods: {
    decr() {
      this.adult += 1;
    },
    incr() {
      this.adult -= 1;
    },
    toggleChildrenOpened() {
      this.isChildrenOpened = !this.isChildrenOpened
    },
    pushChild(option) {
      this.children.push(option);
      console.log('pushChild', option);
    }
  }

}
</script>

<style lang="scss">
$b: '.select';

#{$b} {
  $a-blue: #2b51e7;
  max-width: 250px;
  margin-right: 25px;
  position: relative;

  .input,
  &__input {
    padding: 0 6px;
    border: 1px solid #ddd;
    font-size: 14px;
    height: 38px;
    border-radius: 4px;
    display: flex;
    align-items: center;
    justify-content: center;
    position: relative;

    &:hover {
      border-color: $a-blue;
      cursor: pointer;
    }

    &._active {
      border-color: $a-blue;
    }
  }

  &__top {
    margin-bottom: 15px;
  }

  &__body {
    padding: 10px;
    border: 1px solid $a-blue;
    border-radius: 4px;
    position: absolute;
    top: 110%;
    min-width: 200px;
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  &__adult {
    margin-bottom: 10px;
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: center;

    &-btn {
      width: 26px;
      height: 26px;
      border: 1px solid #ddd;
      border-radius: 100%;
      display: flex;
      align-items: center;
      justify-content: center;

      svg {
        width: 12px;
        height: 12px;
      }

      &:hover {
        border-color: $a-blue;
        cursor: pointer;
      }
    }

    &-content {
      margin: 0 15px;
      display: inline-block;
    }
  }

  &__children {
    width: 100%;
   
    &.input {
      padding: 0;
      position: relative;
    }
  }

  &__age {
    padding: 15px;
    top: 100%;
    left: 0;
    width: 100%;
    background-color: #fff;
    z-index: 5;
    overflow-y: scroll;
    height: 200px;
    flex-direction: column;
    position: absolute;
    align-items: flex-start;
    justify-content: flex-start;
    border: 1px solid #ddd;
    border-radius: 4px;

    &::-webkit-scrollbar {
      width: 0;
      display: none;
    }

    li {
      font-size: 14px;
      padding: 5px;
    }
  }


  
  ul {
    padding: 0;
    margin: 0;
  }

  li {
    list-style: none;
    // padding: 0;
  }
  &__children-item {
    color: #2b51e7;
  }
}

</style>