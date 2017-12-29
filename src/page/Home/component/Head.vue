<style lang="less" scoped>
  .Head {
    height: 80px;
    width: 100%;
    text-align: center;
    box-shadow: 0px 1px 1px #ccc;
    .content {
      margin: 0 auto;
      height: 100%;
      width: 100%;
      max-width: 1200px;
      display: flex;
      justify-content: space-between;
      .left {
        display: flex;
        img {
          height: 60px;
          margin-top: 10px;
        }
        .language{
         margin-top: 40px;
         margin-left: 10px;
       }
      }
      .right {
        display: flex;
        //flex-direction: column;
        .menu {
          margin-top: 30px;
          width: auto;
          height: 40px;
          display: flex;
          .item {
            padding: 0 15px;
            height: 100%;
            line-height: 40px;
            font-size: 15px;
            &:hover {
              cursor: pointer;
            }
          }
          .active {
            color: #2098D1;
          }
        }
      }
    }
  }
</style>

<template>
  <nav class="Head">
    <!--内容区域   最大1200px-->
    <div class="content">
      <!--左边区域-->
      <div class="left">
        <img :src="logo" alt="格兰菲德科技">
        <!--语言切换-->
        <Dropdown class="language" trigger="click" @on-click="languageChange">
          <a href="javascript:void(0)">
            {{ language == 'CN' ? '中文' : 'English' }}
            <Icon type="arrow-down-b"></Icon>
          </a>
          <DropdownMenu slot="list">
            <DropdownItem :selected="language == 'CN'" name="CN">中文</DropdownItem>
            <DropdownItem :selected="language == 'EN'" name="EN">English</DropdownItem>
          </DropdownMenu>
        </Dropdown>
      </div>
      <!--右边区域-->
      <div class="right">
        <!--菜单-->
        <div class="menu">
          <div class="item hvr-underline-reveal" v-for="item in menuList"
               :class="item.value == activeMenu ? 'active' : ''" @click="menuClick(item.value)">
            {{ $t(item.name) }}
          </div>
        </div>
      </div>
    </div>
  </nav>
</template>

<script>
  import logo from '../../../assets/logo.png'

  export default {
    name: 'Head',
    data () {
      return {
        logo: logo,
        menuList: this.mydata.menulist,
        activeMenu: 'home',
        language: 'CN'
      }
    },
    methods: {
      menuClick (value) {
        this.activeMenu = value
      },
      languageChange (name) {
        this.$i18n.locale = name
        this.language = name
      }
    }
  }
</script>
