<template>
  <div id="app">
    <div class="header header-fixed unselectable header-animated">
        <div class="header-brand">
            <div class="nav-item no-hover">
                <h6 class="title">Решение</h6>
            </div>
            <div class="nav-item nav-btn" id="header-btn">
                <span></span>
                <span></span>
                <span></span>
            </div>
        </div>
        <div class="header-nav" id="header-menu">
            <div class="nav-left">
                <div class="nav-item text-center">
                    <a href="#">
                        <span class="icon">
                            <i class="fab fa-wrapper fa-twitter" aria-hidden="true"></i>
                        </span>
                    </a>
                </div>
            </div>
            
            <div class="nav-right">
                <div class="nav-item has-sub toggle-hover" id="dropdown">
                    <a class="nav-dropdown-link">Методы принятия решений</a>
                    <ul class="dropdown-menu dropdown-animated" role="menu">
                        <router-link :to="{name: 'Detail'}">Детализация</router-link>
                        <li role="menu-item"><a href="#">Шкала</a></li>
                        <li role="menu-item"><a href="#">Квадрат Декарта</a></li>
                        <li role="menu-item"><a href="#">SWOT-анализ</a></li>
                        <li role="menu-item"><a href="#">Стол менторов</a></li>
                        <li role="menu-item"><a href="#">Приоритизация</a></li>
                    </ul>
                </div>
            </div>
        </div>
    </div>

    <router-view />
    
  </div>
</template>

<style lang="scss">
</style>
