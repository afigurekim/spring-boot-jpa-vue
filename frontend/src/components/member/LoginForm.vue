<template>
<div>
  <Nav></Nav>
  <form @submit="submitbtn" action="/memberlist">
    <div class="form-group">
      <label for="email">이메일:</label>
      <input type="email" v-model="email" class="form-control" id="email" placeholder="이메일 예: id@domain.com">
      <ul class="validation-errors">
        <li v-if="!validation.email.format">이메일 주소 형식에 어긋납니다</li>
        <li v-if="!validation.email.required">이메일 주소를 입력해주세요</li>
      </ul>
    </div>
    <div class="form-group">
      <label for="password">패스워드:</label>
      <input type="password" v-model="password" class="form-control" id="password" placeholder="패스워드 예: password">
      <ul class="validation-errors">
          <li v-if="!validation.password.required">패스워드를 입력해주세요</li>
      </ul>
    </div>
    <div class="checkbox">
      <label><input type="checkbox"> Remember me</label>
    </div>
    <button type="submit" class="btn btn-default">로그인</button>
  </form>
  <Footer></Footer>
</div>
</template>

<script>
import Nav from '@/components/common/Nav.vue'
import Footer from'@/components/common/Footer.vue'
import axios from 'axios'

const REGEX_EMAIL = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/
const required = val => !!val.trim()

export default {
  components: {
    Nav,
    Footer
  },
  data() {
      return {
          email: '',
          password: '',
          validchk: false
      }
  },
  computed: {
      validation() {
          return {
              email: {
                  required: required(this.email),
                  format: REGEX_EMAIL.test(this.email)
              },
              password: {
                  required: required(this.password)
              }
          }
      },
      valid() {
          const validation = this.validation
          const fields = Object.keys(validation)
          let valid = true
          for (let i = 0; i < fields.length; i++) {
              const field = fields[i]
              valid = Object.keys(validation[field]).every(key => validation[field][key])
              if (!valid) { break }
          }
          return valid
      },
      noLogin() { return !this.valid || this.validchk }
  },
  methods: {
    // submitbtn:function(e) {
    //     if (!this.noLogin && this.email === 'home@home.com' && this.password === '1234') {
    //         this.validchk = true
    //         alert(`${this.email}\n${this.password}\n로그인 성공`)
    //     } else {
    //         alert('로그인 실패')
    //         e.preventDefault()
    //     }
    // }
    submitbtn: function() {
      alert('클릭')
      axios.get('/customers/count')
      .then(d => { alert(`SUCCESS : ${d.data}`) })
      .catch(e => { alert('ERROR') })
    }
  }
}
</script>

<style scoped>
ul {
    list-style-type: none;
    padding: 0;
    margin: 0.25em 0;
}
ul li {
    font-size: 0.5em;
}
.validation-errors {
    height: 32px;
}
</style>