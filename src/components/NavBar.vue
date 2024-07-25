<template>
    <div class="app-navbar">

      <img src="../assets/logo.png" class="logo">

      <el-menu
        :default-active="activeIndex"
        class="el-menu-demo"
        mode="horizontal"
        background-color="#545c64"
        text-color="#fff"
        active-text-color="#ffd04b"
      >
      </el-menu>
      <div class="navbar-search">
        <el-input
          placeholder="Search mails..."
          suffix-icon="el-icon-search"
          v-model="searchQuery">
        </el-input>
      </div>
      <div class="navbar-notification">
        <el-badge :value="newEmailCount" class="item">
          <el-button icon="el-icon-bell" circle></el-button>
        </el-badge>
      </div>
    </div>
  </template>

  <script>
  export default {
    data() {
      return {
        activeIndex: 'inbox',
        searchQuery: '',
        newEmailCount: 240, 
      };
    },
    methods: {
    }
  };
  </script>
  
  <style scoped>
  .app-navbar {
    padding: 4px 0;
    display: flex;
    justify-content: space-between; 
    align-items: center; 
    background-color: #d8491de0;
  }
  
  .logo {
    height: 50px;
    margin-left: 20px;
  }
  
  .navbar-search {
    width: 50%;
    text-align: center;
    margin: 0 20px; 
  }
  
  .navbar-notification {
    margin-top: 5px;
    margin-right: 35px; 
  }
  
  </style>
  