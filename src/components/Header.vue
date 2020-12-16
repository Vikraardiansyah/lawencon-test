<template>
  <header>
    <div class="header-top">
      <b-container>
        <b-row>
          <b-col md="6">
            <img src="../assets/redbus_india_logo.png" alt="redbus" />
          </b-col>
          <b-col md="6">
            <p>
              <span class="login"> Login</span>
              <span class="login"> Sign Up</span>
            </p>
          </b-col>
        </b-row>
      </b-container>
    </div>
    <div class="menu">
      <b-container>
        <b-row class="justify-content-center">
          <b-col md="7">
            <ul>
              <li>Home</li>
            </ul>
          </b-col>
        </b-row>
      </b-container>
    </div>
  </header>
</template>

<script>
export default {
  name: 'Header',
};
</script>

<style>
.header-top {
  background: #fff;
  border-top: 3px solid coral;
}

.header-top p {
  float: right;
}

.header-top img {
  width: 100px;
}

.login {
  background: coral;
  color: #fff;
  float: right;
  padding: 3px 20px;
  margin: 10px;
}

ul {
  padding: 0;
  margin: 0;
}
.menu ul {
  margin-bottom: 0px;
}

li {
  list-style: none;
}

.menu {
  background: coral;
}

.menu ul li {
  padding: 10px 20px;
  display: inline-block;
  color: #fff;
  cursor: pointer;
}
</style>
