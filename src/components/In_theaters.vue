<template>
          <!--电影列表开始-->
        <div class="list in_theaters">
            <ul>
                
                <li v-for="item in subjects">
                    <a href="#/details">
                        <img :src="item.images.large" alt="">
                    </a>
                    <div class="meta">
                        <h4><span>{{item.title}}</span> <em>{{item.rating.average}}分</em></h4>
                        <div class="otherinfo">类型:<span v-for="a in item.genres">{{a}}</span></div>
                    </div>
                </li>

            </ul>
            <div class="paging">
                <label>总共：0条记录,第0/0页;</label>
                <!-- 加上disable类样式，表示按钮禁用状态 -->
                <button class="prev disable ">上一页</button>
                <button class="next">下一页</button>
            </div>
        </div>
        <!--电影列表结束-->
</template>

<script>
import jsonp from 'jsonp'
export default {
  name: 'in_theaters',
  created(){
    this.fetchData();
  },
  data () {
    return {
      subjects:[]
    }
  },
  methods:{
      fetchData(){
          var that = this;
          jsonp('https://api.douban.com/v2/movie/in_theaters?count=20&start=1', null, function (err, data) {
            if (err) {
                console.error(err.message);
            } else {
                console.log(data.subje);
                that.subjects = data.subjects;
                console.log(that.subjects)
            }
            });
      }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
