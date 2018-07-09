# Vue路由传参

<div v-for="item in data" :key="item.id" @click="goDetail(item.id)"></div>

1.路由id
// 当前页面
methods: {
  goDetail (id) {
    this.$router.push({path:`/detail/${id}`})
  }
}
// 路由配置
{
   name:'management-detail',
   path:'detail/:id?',
   meta:{
     title:'商品详情',
     keepAlive: false // 需要被缓存
   },
   component:resolve => require(['business/management/detail/detail.vue'],resolve)
 }
// 详情页
created () {
  this.id = this.$route.params.id
}
// 这就需要在path上添加/:id 
2.路由name + params
// 当前页面
methods: {
  goDetail (id) {
    this.$router.push({name:'management-detail', params:{id: id}})
  }
}
// 路由配置
{
   name:'management-detail',
   path:'detail',
   meta:{
     title:'商品详情',
     keepAlive: false // 需要被缓存
   },
   component:resolve => require(['business/management/detail/detail.vue'],resolve)
 }
// 详情页
created () {
  this.id = this.$route.params.id
}
// path不用添加id 这相当于post请求，不会在请求地址栏中看到参数
3.路由path + query
// 当前页面
methods: {
  goDetail (id) {
    this.$router.push({path:'detail', query:{id: id}})
  }
}
// 路由配置
{
   name:'management-detail',
   path:'detail',
   meta:{
     title:'商品详情',
     keepAlive: false // 需要被缓存
   },
   component:resolve => require(['business/management/detail/detail.vue'],resolve)
 }
// 详情页
created () {
  this.id = this.$route.query.id
}
// path不用添加id 这相当于get请求，会在请求地址栏中看到请求参数