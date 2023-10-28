<script setup>

import Exit from "@/components/icons/exit.vue";
import MenuIcon from "@/components/icons/menu-icon.vue";
</script>

<template>
  <header class="header">
    <div class="container">
      <div class="header-wrapper">
        <ul class="header-list">
          <li><a href="#">Билеты и абонементы</a></li>
          <li><a href="#">Как купить?</a></li>
          <li><a href="#">Правила</a></li>
          <li><a href="#">Возврат билетов</a></li>
          <li><a class="header-exit" href="#">
            <exit/>
            <div>Войти</div>
          </a></li>
        </ul>
        <div class="header-menu">
          <menu-icon/>
        </div>
      </div>
    </div>
  </header>
</template>

<style scoped lang="scss">
.header {
  padding: 2rem 0;
  position: fixed;
  top: 0;
  width: 100%;
  z-index: 100;

  &-wrapper {
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 2rem;
  }

  &-list {
    display: flex;
    align-items: center;
    justify-content: space-between;
    flex: 1 1 0;
    font-size: 1.5rem;

    li:first-child{
      text-transform: uppercase;
    }

    a{
      display: flex;
      align-items: center;
      gap: 0.5rem;
    }
  }

  &-exit {
    display: flex;
    gap: 0.5rem;
  }
}

.container {
  padding: 0 2rem;
}

</style>