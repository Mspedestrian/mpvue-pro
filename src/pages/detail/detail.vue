<template>
<div v-if="detailObj">
    <div class="top">
        <!-- <div style="height: 220px;overflow: hidden;"></div> -->
        <image :src="detailObj.images.large" alt="" style="width: 100%;height: 220px"></image>
        <div class="back"></div>
        <div class="top-content flex-wrap flex-ac">
            <div class="left">
                <image :src="detailObj.images.large" alt="" style="width:120px;height: 180px"></image>
            </div>
            
            <div class="right">
                <p class="title midf show-ellipsis">{{detailObj.title}}</p>
                <p class="sm-title midf show-ellipsis">{{detailObj.original_title}}</p>
                <div class="flex-wrap flex-ac">
                    <p class="bigf">{{detailObj.rating.average}}</p>
                    <div>
                        <p>xingxing</p>
                        <p class="smf">{{detailObj.reviews_count}}人评价</p>
                    </div>
                </div>
                
            </div>
        </div>
    </div>


    <div class="con-line">
        <p>{{genres}}</span></p>
        <p>{{detailObj.year}}上映 <span>{{countries}}</span></p>
        <p><span v-for='item in detailObj.directors'>{{item.name}}</span>(导演) / <span v-for='item in detailObj.casts'>{{item.name}}</span></p>
        <div class="flex-wrap btn-click flex-jb">
            <button>想看</button>
            <button>看过</button>
        </div>
        <div class="grey-title show-ellipsis">{{detailObj.title}}的剧情简介</div>
        <pre>{{detailObj.summary}}</pre>
        <div class="grey-title show-ellipsis">短评</div>
    </div>
    
</div>
</template>

<script>


export default {
    data () {
        return {
            detailObj:null,
        }
    },

    components: {
        
    },
    computed:{
        genres(){
            if(this.detailObj){
                return this.detailObj.genres.join(' / ')
            }
            
        },
        countries(){
            if(this.detailObj){
                return this.detailObj.countries.join(' / ')
            }
            
        }
    },
    methods: {
        
        getShortCommentsList(id, callback){
            let vm = this;
            wx.request({
                url: `http://t.yushu.im/v2/movie/subject/${parseInt(id)}/comments`,
                // data: {
                //     x: '',
                //     y: ''
                // },
                header: {
                    'content-type': 'application/json' // 默认值
                },
                success: function (res) {
                    console.log(res.data)
                    vm.setData({
                        shortCommentsList: res.data
                    })
                    callback && callback(res.data);
                }
            })
        },
        getDetailById(id,callback){
            let vm = this;
            wx.request({
                url: `http://t.yushu.im/v2/movie/subject/${parseInt(id)}`,
                header: {
                    'content-type': 'application/json' // 默认值
                },
                success: function (res) {
                    vm.detailObj = res.data;
                    console.log(res.data)
                    callback && callback(res.data);
                }
            })
        },
        
    },
    mounted(){
        this.getDetailById(this.$root.$mp.query.id);
        // this.getDetailById(7);
    },

    created () {
        // 调用应用实例的方法获取全局数据
        
    }
}
</script>

<style scoped lang="less">
.top {
    width: 100%;
    height: 260px;
    position: relative;
    .back {
        position: absolute;
        top:0;
        left:0;
        background: black;
        opacity: .8;
        height: 220px;
        width: 100%;

    }
    
}  
.top-content {
    position: absolute;
    top:60px;
    left: 10px;
    color:white;
    .title {
        width: 130px;
    }
    .sm-title {
        
    }
} 
.left {
    margin-right: 10px;
}
.show-ellipsis {
    text-overflow: ellipsis;
    white-space: nowrap;
    overflow: hidden;
    width: 200px;
}
.btn-click {
    margin-top: 10px;
    margin-bottom: 10px;
    button {
        width: 48%;
        border: 1px solid #ff7800;
        color:#ff7800;
        background: white;
    }
}
.grey-title {
    color:#aaa;
    width: 100%;
    margin-top: 30px;
    margin-bottom: 10px;
}
</style>
