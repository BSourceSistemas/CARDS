---
layout: minimal
title: Contato
description: Duvidas? Fale conosco.
permalink: /contato/
---

<style type="text/css" media="screen">
  .container {
    margin: 0px auto;
    max-width: 600px;
  }
</style>

<div class="container">

  <h2>Fale com a nossa equipe</h2>

  <div id="form" class="contact-form">
    <form accept-charset="UTF-8" method="POST" action="https://blog.bsource.com.br/contato/mensagem-enviada/" 
    v-on:submit.prevent="validateBeforeSubmit" ref="contact">
      <fieldset>
        <input type="hidden" name="_subject" value="Novo Contato!" />
        <input type="hidden" name="_next" value="{{ site.url }}/contato/mensagem-enviada/" />
        <input type="hidden" name="_language" value="en" />

        <input type="text" name="name" placeholder="Seu Nome" v-validate="'required'"
               :class="{ 'has-error': errors.has('name') }">
        <span v-if="errors.has('name')" v-cloak>${ errors.first('name') }</span>

        <input type="text" name="email" placeholder="Seu e-mail" v-validate="'required|email'"
               :class="{ 'has-error': errors.has('email') }">
        <span v-if="errors.has('email')" v-cloak>${ errors.first('email') }</span>

        <!--Importando Script Jquery-->
<script type="text/javascript" src="https://code.jquery.com/jquery-3.2.1.min.js"></script>
        <textarea name="message" onkeyup="adjust_textarea(this)" placeholder="Sua Mensagem" v-validate="'required'"
                  :class="{ 'has-error': errors.has('message') }"></textarea>
        <span v-if="errors.has('message')" v-cloak>${ errors.first('message') }</span>
        <button type="submit">Enviar</button>
      </fieldset>
    </form>
  </div>

</div>

<script src="https://unpkg.com/vue@2.4.2"></script>
<script src="https://unpkg.com/vee-validate@2.0.0-rc.8"></script>
<script type="text/javascript">
Vue.use(VeeValidate);

new Vue({
  el: '#form',
  delimiters: ['${', '}'],
  methods: {
    validateBeforeSubmit: function () {
      this.$validator.validateAll();
      if (!this.errors.any()) {
        this.$refs.contact.submit();
      }
    }
  }
});
</script>