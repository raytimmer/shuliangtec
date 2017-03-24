<template>
  <div class="hello">
    <nav class="list">
      <ul class="yiji">
        <li v-for="value in items.children" class="dropdown">
          <a :value="value.id" @click.stop="menuClick(value)">
            {{value.name}}
            <i class="fa fa-chevron-down" v-if="!value.leaf"></i>
            <i class="fa fa-chevron-up" v-if="value.leaf"></i>
          </a>
            <ul class="erji dropdown-menu">
                <li v-for="value2 in value.children">
                  <a :value="value2.id" @click.stop="menuClick(value2)">
                    {{value2.name}}
                    <i class="fa fa-caret-down" v-if="!value2.leaf"></i>
                    <i class="fa fa-caret-up" v-if="value2.leaf"></i>
                  </a>
                  <ul class="sanji dropdown-menu">
                    <li v-for="value3 in value2.children">
                      <a :value="value3.id" v-text="value3.name"></a>
                    </li>
                  </ul>
                </li>
            </ul>
        </li>
      </ul>
    </nav>
  </div>
</template>
<script>
  import axios from 'axios';
  var url='http://plat.idx365.com/interfaceApiSendData.do?username=apiTest&password=apiTest&type=read&data=1000&operate=%E6%B5%A6%E6%B1%9F%E6%B0%B4%E6%99%B6%E4%BA%A7%E5%93%81%E4%BB%B7%E6%A0%BC%E6%8C%87%E6%95%B0';
export default {
  data () {
    return {
      item: '',
      show:false
    }
  },
  created () {
    var _this = this;
    axios.get(url).then(function (response) {
      var data = response.data.data[0].data;
      _this.item = data
      // console.log(_this.item.children)
    });
  },
  methods: {
    menuClick:function (value) {
      value.leaf = !value.leaf
      var oul = event.target.parentNode.lastChild
      if(value.leaf){
          oul.className = 'dropdown-menu show';
      }else{
        oul.className = 'dropdown-menu hide';
      }
    }
  },
  computed: {
    items: function () {
      return this.item
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.list{
  width: 270px;
  margin:0px auto 0 auto;
  text-align: left;

}
.list>ul{
  border: 1px solid #ddd;
  border-radius: 4px
}
.list ul{
  margin: 0;
  padding: 0;
  list-style: none;
  background: #fff;
}
.list ul li{
  border-bottom:solid 1px #d1d1d3;
  cursor: pointer;
}
.list ul li a{
  padding-left: 30px;
  color:#525252;
  font-size:16px;
  font-weight:bold;
  height:36px;
  line-height: 36px;
  position: relative;
  outline:none;
  overflow: hidden;
  white-space: nowrap;
  text-overflow:ellipsis;
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.list ul li a>i{
  margin-right: 20px;
}
.list ul li ul{
  overflow: hidden;
  background: #444359;
}
.list ul li ul li{

}
.list ul li ul li ul{
  background: #a12c22;
}
.list ul li ul li a{
  color: #d9d9d9;
  margin-left:20px;

}
.list ul li ul li ul li {
  background-color: #b63b4d;

}
.list ul li ul li ul li a{
  margin-left:40px;
  color: #fff;
}
.dropdown .dropdown-menu {
  max-height: 0;
  overflow: hidden;
  list-style: none;
  padding: 0;
  margin: 0;
}
.dropdown .show, .dropdown .hide {
  -moz-transform-origin: 50% 0%;
  -ms-transform-origin: 50% 0%;
  -o-transform-origin: 50% 0%;
  -webkit-transform-origin: 50% 0%;
  transform-origin: 50% 0%;
}
.dropdown .show {
  display: block;
  max-height: 9999px;
  -moz-transition: max-height 13s ;
  -o-transition: max-height 13s ;
  -webkit-transition: max-height 13s ;
  transition: max-height 13s ;
}
.dropdown .hide {
  max-height: 0;
  /*-moz-transform: translateY(1);
  -ms-transform: translateY(1);
  -o-transform: translateY(1);
  -webkit-transform: translateY(1);
  transform: translateY(1);*/
  -moz-transition: max-height 13s ;
  -o-transition: max-height 13s ;
  -webkit-transition: max-height 13s ;
  transition: max-height 13s ;
  transition-delay: .2s;
  -moz-transition-delay: .2s; /* Firefox 4 */
  -webkit-transition-delay: .2s; /* Safari 和 Chrome */
  -o-transition-delay: .2s;
}
</style>
