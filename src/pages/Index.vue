<template>
  <div class="q-pa-md" >

    <div class="row">
      <h1 class="title">Você tambem odeia adicionar contatos antes de usar o chat no WhatsApp?</h1>
    </div>

    <div class="row">
      <div class="col-12 text-center">
        <img alt="No Contact" src="~assets/no-contact.png" class="no-contact" />
      </div>
    </div>

    <div class="row">
      <p>Informe o número abaixo para conversar</p>
    </div>

    <div class="row text-center">
      <q-input
        type="tel"
        v-model="whatsNumber"
        label="Informe o número do Whats"
        class="col-12"
        @input="enterNumber"
        v-mask="['(##) #####-####']"
      >
        <template v-slot:prepend>
          <q-icon name="phone" />
        </template>
      </q-input>
    </div>

    <div class="row" v-if="numberFilled">
      <div class="col-12 text-center">
        <a :href="apiHrefNumber" target="_new">
          <img alt="WhatsApp Button" src="~assets/whatsapp.png" class="whatsAvatar">
        </a>
      </div>
    </div>

  </div>
</template>

<style>

  .title {
    font-size: 2em;
    line-height: 3rem;
    text-align: center;
  }

  .no-contact {
    width: 180px;
  }

  .whatsAvatar {
    padding-top: 15px;
  }

</style>

<script>

import { mask } from 'vue-the-mask'

export default {
  name: 'SemTempoIrmao',
  data () {
    return {
      whatsNumber: '',
      apiHrefNumber: '',
      numberFilled: false
    }
  },
  methods: {
    enterNumber () {
      const whatsNumber = this.whatsNumber.replace(/[^0-9]/g, '')

      // Early return
      if (whatsNumber.length !== 11) {
        this.numberFilled = false
        return false
      }
      this.numberFilled = true

      this.apiHrefNumber = 'http://api.whatsapp.com/send?1=pt_BR&phone=55' + whatsNumber

      /*
      // Focus to Hide Keyboard
      let field = document.createElement('input')
      field.setAttribute('type', 'text')
      document.body.appendChild(field)

      setTimeout(function () {
        field.focus()
        setTimeout(function () {
          field.setAttribute('style', 'display:none;')
        }, 50)
      }, 50)
      */

      return false
    }
  },
  directives: {
    mask
  }

}
</script>
