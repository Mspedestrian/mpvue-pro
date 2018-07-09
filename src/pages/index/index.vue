<template>
<div>
    <div class="top">
        <input type="text" name="">
    </div>
    <div class="list-item">
        <div class="title">
            <div class="line"></div>
            <span>豆瓣Top250</span>
        </div>
        <scroll-view scroll-x style="padding-left: 10px;padding-right: 10px;box-sizing: border-box;">
            <div style="display: flex;">
                <div class="video-item" v-for="item in top250List" @click="goDetail(item)">
                    <image :src="item.images.large" alt="" style="width:165px"></image>
                    <p class="video-title">{{item.title}}</p>
                </div>
            </div>
            
       
        </scroll-view>
    </div>
    
</div>
</template>

<script>


export default {
    data () {
        return {
            top250List:[],
        }
    },

    components: {
        
    },

    methods: {
        
        getTop250List(){
            let vm = this;
            wx.request({
                url: 'http://t.yushu.im/v2/movie/in_theaters',    // 拼接完整的url
                // data: 
                method:'GET',
                header: {
                    'content-type': 'application/json'
                },
                success(res) {
                    // resolve(res.data)  // 把返回的数据传出去
                    console.log(res);
                    vm.top250List = res.data.subjects
                },
                fail(ret) {
                    // reject(ret)   // 把错误信息传出去
                }
            })
        },
        goDetail(item){
            wx.navigateTo({
              url:`/pages/detail/main?id=${item.id}`
            })
        },
        
    },
    mounted(){
        this.getTop250List();
    },

    created () {
        // 调用应用实例的方法获取全局数据
        
    }
}
</script>

<style scoped lang="less">
    .top {
        background: #00b51d;
        height: 48px;
        padding: 10px;
        box-sizing: border-box;
        input {
            background: white;
            border-radius: 5px;
        }
    }
    .title {
        display: flex;
        height: 30px;
        margin-top: 10px;
        margin-bottom: 10px;
        .line {
            width: 5px;
            height: 26px;
            background: #00b51d;
            margin-right: 10px;
        }

    } 
    .video-title {
        text-overflow: ellipsis;
        overflow: hidden;
        width:150px;
        white-space: nowrap;
    }
    .video-item {
        margin-right: 10px;
    }
</style>
