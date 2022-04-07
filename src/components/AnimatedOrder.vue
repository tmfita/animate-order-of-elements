<script setup>
  import {ref, computed, onMounted} from 'vue'

  const systems = [
    {key:0, name:'A'},
    {key:1, name:'B'},
    {key:2, name:'C'},
    {key:3, name:'D'},
    {key:4, name:'E'},
    {key:5, name:'F'}
  ]
  let activeSystem = ref(0)
  const isActive = (key) => {
    if(key==activeSystem.value) {
      return true
    } else {
      return false
    }
  }
  const nodes = ref('')
  onMounted(()=>{
    nodes.value = document.querySelectorAll(".system-icon");
    nodes.value.forEach((node,i)=>{
      if(i==1) {
        node.style.left = '45px'
      } else if(i>1) {
        node.style.left = `${45+(45*(i-1))}px`
      }
    })
  })
  
  const changeActiveSystem= (key) => {
    const previousKey = activeSystem.value
    activeSystem.value = key;
    nodes.value.forEach((elem, index)=>{
      if(index==key) {
        nodes.value[index].style.left = '-7px'
      } else if(!(index>key&&index>previousKey)&&!(index<key&&index<previousKey)) {
        if(index==previousKey) {
          if(index<key) {
            nodes.value[index].style.left= `${45+(45*index)}px`
          } else if(index>key) {
            nodes.value[index].style.left= `${45+(45*(index-1))}px`
          }
        } else if(index>previousKey) {
          nodes.value[index].style.left= `${45*(index+1)}px`
        } else if(index<previousKey) {
          nodes.value[index].style.left= `${45*(index)}px`
        }
      }
      
    })
  }
</script>
<template>
  <div class="system-list">
    <div
      class="system-icon"
      :class="{'active': isActive(system.key)}"
      v-for="system in systems"
      @click="changeActiveSystem(system.key)"
    > 
      {{system.key}}
    </div>
  </div>
</template>
<style lang="scss" scoped>
  .system-list {
    display:flex;
    align-items:center;
    gap: 10px;
    margin-bottom: 5px;
    height:45px;
    margin-left: 100px;
    position: relative;
    .system-icon {
      background: white;
      width: 35px;
      height: 35px;
      border-radius: 50%;
      display:flex;
      align-items:center;
      justify-content:center;
      cursor: pointer;
      transition: .3s;
      position:absolute;
      border: 1px solid black;
      &.active {
        width: 40px;
        height: 40px;
      }
      
    }
  }
</style>