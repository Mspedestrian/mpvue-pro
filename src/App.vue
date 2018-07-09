<script>
export default {
  created () {
    // 调用API从本地缓存中获取数据
    const logs = wx.getStorageSync('logs') || []
    logs.unshift(Date.now())
    wx.setStorageSync('logs', logs)

    console.log('app created and cache logs by setStorageSync')
  }
}
</script>

<style>
.container {
  /*height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
  padding: 200rpx 0;
  box-sizing: border-box;*/
}
/* this rule will be remove */
* {
  transition: width 2s;
  -moz-transition: width 2s;
  -webkit-transition: width 2s;
  -o-transition: width 2s;
  margin:0;
  padding: 0;
  font-size: 15px;
}
html,
body {
  font-size: 15px;
  width: 100%;
  overflow: hidden;
}
.con-line {
  width: 100%;
  box-sizing: border-box;
  padding-left: 10px;
  padding-right: 10px;
}
.flex-wrap {
  display: flex;
}
.flex-ac {
  align-items: center;
}
.flex-jb {
  justify-content: space-between;
}
.bigf {
  font-size: 40px;
}
.midf {
  font-size: 24px;
} 
.smf {
  font-size: 13px;
}
</style>
