<template>
  <div class="hello">
    <!--items:{{item}}-->
    <nav id="sshyd" class="list">
      <ul class="yiji">
        <li v-for="value in items.children">
          <a :value="value.id" v-text="value.name" @click.stop="menuClick(value)"></a>
          <transition
            name="animated"
            enter-active-class="animated slideInDown"
            leave-active-class="animated slideOutUp"
          >
          <ul class="erji " style="overflow: hidden; padding-top: 0px; padding-bottom: 0px; display: none;" v-show="value.leaf">
            <li v-for="value2 in value.children">
              <a :value="value2.id" v-text="value2.name" @click.stop="menuClick(value2)"></a>
              <ul class="sanji" v-show="value2.leaf">
                <li v-for="value3 in value2.children">
                  <a :value="value3.id" v-text="value3.name"></a>
                </li>
              </ul>
            </li>
          </ul>
          </transition>
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
    })

  },
  methods: {
    menuClick:function (value) {
      // console.log(event.target.parentNode)
      // this.show = !this.show
      // console.log(event);
      value.leaf = !value.leaf
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
.list ul{
  margin: 0;
  padding: 0;
  list-style: none;
}
.list ul li{
  border:solid 1px #d1d1d3;
  cursor: pointer;
}
.list ul li a{
  padding-left: 30px;
  color:#525252;
  font-size:16px;
  display: block;
  font-weight:bold;
  height:36px;
  line-height: 36px;
  position: relative;
  outline:none;
  overflow: hidden;
  white-space: nowrap;
  text-overflow:ellipsis;
}
.list ul li .inactives{
  text-decoration:underline;
  color:#d94f5c;
}
.list ul li ul li .lia_l{
  text-decoration:underline;
  color:#d94f5c;
}
.list ul li ul{
  /*display: none;*/
}
.list ul li ul li{
  border-left:0;
  border-right:0;
  background-color:#fff;
  border-color:#d1d1d3;
}
.list ul li ul li ul{
  /*display: none;*/
}
.list ul li ul li a{
  margin-left:20px;

}
.list ul li ul li ul li {
  background-color:#fff;
  border-color:#d1d1d3;
}
.list ul li ul li ul li a{
  margin-left:40px;
}
.erji {
  display: block;
}
</style>
