<template>
  <div class="container" @click="clickHandle('test click', $event)">
     <button open-type="getUserInfo" @getuserinfo="onGetUserInfo">点击获取用户信息</button>
    <div class="userinfo" @click="bindViewTap"> 
      <img class="userinfo-avatar" v-if="userInfo.avatarUrl" :src="userInfo.avatarUrl" background-size="cover" /> 
      <div class="userinfo-nickname">
        <card :text="userInfo.nickName"></card>
      </div>
    </div>
    <p v-if="Object.keys(scanResult).length">扫码之后的详情：{{scanResult}}</p>
    <button open-type="getUserInfo" @click="scan">扫码</button>
  </div>
</template>

<script>
import card from '@/components/card'

export default {
  data () {
    return {
      motto: 'Hello World',
      userInfo: {},
      scanResult:{}
    }
  },

  components: {
    card
  },

  methods: { 
    bindViewTap () {
      const url = '../logs/main'
      wx.navigateTo({ url })
    },
    onGetUserInfo () { 
      wx.login({
        success: () => {
          wx.getUserInfo({
            success: (res) => {
              this.userInfo = res.userInfo;
              console.log(this.userInfo)
            }
          })
        },
        fail: function () { 
          wx.showModal({
            title: '警告',
            content: '尚未进行授权，请点击确定跳转到授权页面进行授权。',
            success: function (res) {
              if (res.confirm) {
                console.log('用户点击确定')
                wx.navigateTo({
                url: '../tologin/tologin',
                })
              }
            }
          })
          } 
      })
    },
    clickHandle (msg, ev) {
      console.log('clickHandle:', msg, ev)
    },
    scan(){
      wx.scanCode({
        success (res) {
         this.scanResult=res;
        }
      })
    }
  },

  // created () {
  //   // 调用应用实例的方法获取全局数据
  //   this.getUserInfo()
  // }
}
</script>

<style scoped>
.userinfo {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.userinfo-avatar {
  width: 128rpx;
  height: 128rpx;
  margin: 20rpx;
  border-radius: 50%;
}

.userinfo-nickname {
  color: #aaa;
}

.usermotto {
  margin-top: 150px;
}

.form-control {
  display: block;
  padding: 0 12px;
  margin-bottom: 5px;
  border: 1px solid #ccc;
}

.counter {
  display: inline-block;
  margin: 10px auto;
  padding: 5px 10px;
  color: blue;
  border: 1px solid blue;
}
</style>
