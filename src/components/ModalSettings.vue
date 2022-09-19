<template>
  <div class="content">
    <ul>
      <li><a href="#">Edit</a></li>
      <li><a href="#">Delete</a></li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'ModalSettings'
}
</script>

<style scoped lang="scss">

.content{
  position: absolute;
  display: flex;
  justify-content: flex-start;
  align-items: center;
  background-color: white;
  width: 300px;
  height: 50px;
  border: 1px solid black;
}
li{
  list-style-type: none;
}

</style>
