<template>
  <div class="side-nav">
    <ul>
      <li class="nav-item" v-for="item in data">
        <a v-if="!item.path">{{item.name}}</a>
        <a v-else >{{item.title || item.name}}</a>
        <ul class="pure-menu-list sub-nav" v-if="item.children">
          <li class="nav-item" v-for="navItem in item.children">
            <router-link :to="base + navItem.path">{{navItem.title || navItem.name}}</router-link>
          </li>
        </ul>
        <template v-if="item.groups">
          <div class="nav-group" v-for="group in item.groups">
            <div class="nav-group__title">{{group.groupName}}</div>
            <ul class="pure-menu-list">
              <template v-for="navItem in group.list">
                <li
                  class="nav-item"
                  v-if="!navItem.disabled">
                  <router-link :to="base + navItem.path">{{navItem.title}}</router-link>
                </li>
              </template>
            </ul>
          </div>
        </template>
      </li>
    </ul>
  </div>
</template>

<script>
  export default {
    props: {
      data: Array,
      base: {
        type: String,
        default: ''
      }
    },
    data() {
      return {
        highlights: [],
        navState: []
      };
    }
  };
</script>

<style lang="less">
.side-nav {
  width: 25%;
  box-sizing: border-box;
  padding-right: 30px;
  float: left;

  li {
    list-style: none;
  }
  ul {
    padding: 0;
    margin: 0;
    overflow: hidden;
  }

  .nav-item {
    a {
      font-size: 16px;
      color: #5e6d82;
      line-height: 40px;
      height: 40px;
      margin: 0;
      padding: 0;
      text-decoration: none;
      display: block;
      position: relative;
      transition: all .3s;

      &.active {
        color: #20a0ff;
      }
    }
    .nav-item {
      a {
        display: block;
        height: 40px;
        line-height: 40px;
        font-size: 13px;
        padding-left: 24px;


        &:hover {
          color: #20a0ff;
        }
      }
    }
  }
  .nav-group__title {
    font-size: 12px;
    color: #99a9bf;
    padding-left: 8px;
    line-height: 26px;
    margin-top: 10px;
  }
}
</style>
