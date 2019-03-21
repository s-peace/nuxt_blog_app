<template>
  <section class="container">
    <el-card style="flex:1">
      <div slot="header" class="clearfix">
        <span>login</span>
      </div>
      <form action="">
        <div class="form-content">
          <span>user ID</span>
          <el-input placeholder="" v-model="formData.id" />
        </div>
        <div class="form-content">
          <el-checkbox v-model="isCreateMode">
            make account
          </el-checkbox>
        </div>
        <div class="text-right">
          <el-button type="primary" @click="handleClickSubmit">{{buttonText}}</el-button>
        </div>
      </form>
    </el-card>
  </section>
</template>

<script>
import {mapGetters,mapActions} from 'vuex'
import Cookies from 'universal-cookie'

export default {
  asyncData({redirect,store}) {
    if(store.getters['user']){
      redirect('/posts/')
    }
    return {
      isCreateMode: false,
      formData: {
        id: '',
      }
    }
  },
  computed: {
    buttonText() {
      return this.isCreateMode ? 'new register' : 'login'
    },
    ...mapGetters(['user'])
  },
  methods: {
    async handleClickSubmit(){
      const cookies = new Cookies()
      if(this.isCreateMode) {
        try {
          await this.register({...this.formData})
          this.$notify({
            type: 'success',
            title: 'making ur account is success!',
            message: `${this.formData.id} is ur registered account`,
            position: 'bottom-right',
            duration: 1000,
          })
          cookies.set('user',JSON.stringify(this.user))
          this.$router.push('/posts/')
        } catch(e) {
          this.$notify.error({
            title: 'error',
            message: 'this account is already registerd or invalid user id',
            postion: 'bottom-right',
            duration: 1000
          })
        }
      } else {
        try {
          await this.login({...this.formData})
          this.$notify({
            type: 'success',
            title: 'u logined',
            message: `u logined as ${this.formData.id}`,
            position: 'bottom-right',
            duration: 1000,
          })
          cookies.set('user',JSON.stringify(this.user))
          this.$router.push('/posts/')
        } catch(e) {
          this.$notify.error({
            title: 'error',
            message: 'this is invalid user id',
            position: 'border-right',
            duration: 1000,
          })
        }
      }
    },
    ...mapActions(['login','register'])
  }
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.form-content {
  margin: 16px 0;
}

</style>
