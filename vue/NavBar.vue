<template>
  <b-navbar type="light" variant="light" :sticky="true">
    <!-- 网站logo -->
    <b-navbar-brand to="/index">
      <img src="../../assets/images/logo.png" class="logo" alt="图片走丢了"/>
    </b-navbar-brand>
    <!-- 导航栏菜单 -->
    <b-navbar-nav id="navBar" :fill="true" class="ml-auto mr-4">
      <b-nav-item-dropdown text="登录/注销" right>
        <b-dropdown-item>
          <base-router-link
              url="login"
              :params="{admin: false}"
          >登录</base-router-link>
        </b-dropdown-item>
        <b-dropdown-item href="#">
          <base-link
              url="/logout"
              successMessage="注销成功"
              @success="logout"
          >注销</base-link>
        </b-dropdown-item>
      </b-nav-item-dropdown>
      <b-nav-item>
        <base-router-link url="/registerByUser">用户注册</base-router-link>
      </b-nav-item>
      <b-nav-item>
        <base-router-link url="/user/search">用户搜索</base-router-link>
      </b-nav-item>
      <b-nav-item>
        <base-router-link url="/announcement">系统公告</base-router-link>
      </b-nav-item>
      <b-nav-item>
        <base-router-link url="/item/search">项目查询</base-router-link>
      </b-nav-item>
      <b-nav-item>
        <base-router-link url="/item/release">项目发布</base-router-link>
      </b-nav-item>
      <b-nav-item-dropdown text="个人中心" right>
        <b-dropdown-item href="#">
          <base-router-link url="/user/self">个人信息</base-router-link>
        </b-dropdown-item>
        <b-dropdown-item href="#">
          <base-link url="/authenticate" message="认证成功">开发者认证</base-link>
        </b-dropdown-item>
        <b-dropdown-item href="#">
          <base-router-link
              url="userItemSearch"
              :params="{type: 'owner'}"
          >用户中心
          </base-router-link>
        </b-dropdown-item>
        <b-dropdown-item href="#">
          <base-router-link
              url="userItemSearch"
              :params="{type: 'developer'}"
          >开发者中心
          </base-router-link>
        </b-dropdown-item>
        <b-dropdown-item href="#">
          <base-router-link
              url="/user/notification"
          >用户通知
          </base-router-link>
        </b-dropdown-item>
      </b-nav-item-dropdown>
      <b-nav-item href="#">联系客服</b-nav-item>
    </b-navbar-nav>
  </b-navbar>
</template>

<script>
import Login from '../../router/views/common/Login'
import BaseLink from '../base/BaseLink'
import BaseRouterLink from '../base/BaseRouterLink'

export default {
  name: 'nav-bar',
  methods: {
    logout: function () {
      const sessionStorage = window.sessionStorage
      sessionStorage.removeItem('user')
      sessionStorage.removeItem('authorities')
    }
  },
  components: {BaseRouterLink, BaseLink, Login}
}
</script>

<style lang="less" scoped>
  @font-size: 15px;
  .logo {
    width: 50%;
  }
  #navBar a {
    & {
      color: rgba(0, 0, 0, 0.5);
      font-size: @font-size;
    }
    &:hover {
      color: rgb(0, 0, 0);
    }
  }
</style>
