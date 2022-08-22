<template>
<header class="header">
  <div class="header__inner">
    <a href="/" class="header__logo">
      <img src="../assets/icons/logo.svg">
      <h1 class="header__title">ФЛАГ Покупки</h1>
    </a>
    <div class="header__btn">
      <button class="btn" @click="$emit('openModal')">Регистрация</button>
    </div>
  </div>
</header>
</template>

<script>
export default {
  name: 'FHeader',
  props: {

  }
}
</script>

<style scoped>
.header{
  background: #fff;
  box-shadow: 2px 4px 8px rgba(0, 0, 0, 0.1);
  height: 72px;
}
.header__inner{
  max-width: 1208px;
  margin: 0 auto;
  display: flex;
  justify-content: space-between;
  height: 100%;
  align-items: center;
}
.header__logo{
  display: flex;
  cursor: pointer;
  text-decoration: none;
  color: inherit;
}
.header__logo img{
  height: 37px;
  margin-right: 19px;
}
.header__logo h1{
  font-size: 28px;
  line-height: 38px;
}
.btn{
  color: #fff;
  background: #70C05B;
  font-weight: 400;
  font-size: 16px;
  line-height: 150%;
  padding: 8px;
  border: none;
  border-radius: 4px;
  width: 140px;
  cursor: pointer;
}
.btn:hover{
  background: #59a546;
}
.btn:active{
  background: #4c943a;
}
@media(max-width: 1268px){
  .header__inner{
    padding: 0 30px;
  }
}
@media(max-width:500px){
  .btn{
    width: auto;
  }
  .header__title{
    display: none;
  }
}
</style>
