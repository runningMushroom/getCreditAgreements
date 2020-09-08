<template>
  <div class="home">
    <div>
      <label for="clientId">Client ID</label>
      <input id="clientId" type="text" v-model="clientId" placeholder=""/>
    </div>
    <div>
      <label for="loanId">Loan ID</label>
      <input id="loanId" type="text" v-model="loanId" placeholder=""/>
    </div>
    <div>
      <button @click="getCreditAgreement">Get Agreement PDF</button>
    </div>
    <br/>

    <div v-if="b64Data">
      <object class="pdf" :data="b64Data" width="60%" height="800px" />
    </div>    
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'Home',
  components: {
    HelloWorld
  },
  data: () => ({
    loanId: null,
    clientId: null,
    b64Data: null,
  }),
  methods: {
    getCreditAgreement() {
      const axios = require('axios')

      let config = {
        method: 'get',
        url: `https://otptest.lnder.co.za/api/v1/otp/getPreAgreementPdf/${this.clientId}/${this.loanId}`,
      }

      axios(config)
      .then(r => this.b64Data = `data:application/pdf;base64,${r.data}`)
    }
  }
}
</script>
