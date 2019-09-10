<template>

    <div class="q-pa-md fit row inline wrap justify-center items-center content-center ">
  
    <q-layout view="lHh lpr lFf" container style="height: 600px; max-width: 400px;" class="shadow-2 rounded-borders vertical-middle">
      <q-header elevated>
        <q-toolbar>
          <q-avatar>
            <img src="https://cdn.quasar.dev/logo/svg/quasar-logo.svg">
          </q-avatar>

          <q-toolbar-title>
            SignUp
          </q-toolbar-title>

          <q-btn flat round dense icon="whatshot" />
        </q-toolbar>
      </q-header>

      <q-page-container>
        <q-page padding>
          <div class="q-pa-md " style="max-width:400px">

              <q-form @submit="onSubmit" @reset="onReset" class="q-gutter-md">
                <q-input
                  v-model="username"
                  label="Username / Email *"
                  hint="Username / Email"
                  lazy-rules
                  :rules="[ val => val && val.length > 0 || 'Please type something']"
                />
                <q-input
                  v-model="username"
                  label="Username / Email *"
                  hint="Username / Email"
                  lazy-rules
                  :rules="[ val => val && val.length > 0 || 'Please type something']"
                />
                <q-input
                  v-model="username"
                  label="Username / Email *"
                  hint="Username / Email"
                  lazy-rules
                  :rules="[ val => val && val.length > 0 || 'Please type something']"
                />

                <q-input
                  type="password"
                  v-model="password"
                  label="Password *"
                  lazy-rules
                  :rules="[
                    /**val => val !== null && val !== '' || 'Please type your age',
                    val => val > 0 && val < 100 || 'Please type a real age'**/
                  ]"
                />

              <div>
                <q-btn label="Submit" type="submit" color="primary"/>
                <q-btn label="Reset" type="reset" color="primary" flat class="q-ml-sm" />
              </div>
            </q-form>
          </div>
          
          <div class="q-pa-md fit row justify-center items-center  ">
              <q-btn label="Sign-In" type="submit" outline to="/signin"/>
          </div>
        </q-page>
      </q-page-container>
    </q-layout>
  </div>
  
</template>

<script>

export default {
  name: 'SignUp',
  data () {
    return {
      username:'',
      password: '',
      qnotifyDismiss: null
    }
  }, 
  mounted: function () {
    this.$nextTick(function () {
      this.$store.commit('layout/updateDrawerLeftState', false);
      this.$store.commit('layout/updateToolbarBtnMenu', false);  
      this.$q.notify('Seja bem vindo!!!');
    })
  },
  methods: {
    onSubmit () {
      if (this.qnotifyDismiss)
          this.qnotifyDismiss()
      this.qnotifyDismiss= this.$q.notify({
          color: 'negative',
          position: 'top',
          message: 'Loading failed'+ new Date().getTime(1),
          icon: 'report_problem'
        });
        this.loadData();
    },
    onReset () {
      this.username = null
      this.password = null
    },
    loadData () {
      debugger;
      this.$axios.get('fetchApiPolicy').then((response) => {
        var data = response.data
        this.$q.notify({
          color: 'positive',
          position: 'top',
          message: 'Response data',
          icon: 'report_problem'
        })
      }).catch(() => {
        this.$q.notify({
          color: 'negative',
          position: 'top',
          message: 'Loading failed',
          icon: 'report_problem'
        })
      })
    }
  }
}
</script>

<style>
</style>
