<template>
  <nav class='navbar navbar-light bg-light border rounded mt-2'>
    <div class='container-fluid'>

      <a class='navbar-brand' href='#'>
        <i class='bi bi-book-half'></i>
        HAUSAUFGABE 4
      </a>

      <div>
        <!-- TODO: implement -->
        <!-- <img src='@/assets/ButtonDarkMode.jpg' width ='114' class='rounded float-end' alt='' id="btn-dark-mode"> -->
       

        <button class='btn btn-primary me-3' type='submit' @click='toggleTests' >
          <i class='bi bi-robot'></i>
          {{ (!testsOpen) ? "Run tests" : "Close tests" }}
        </button>

         <button id="btn-dark-mode" @click="toggleDarkMode">{{isDark?"Lights on" :"Lights off"}}</button>
      </div>

    </div>
  </nav>  
</template>

<script>
export default {
  name: 'NavBar',
  props: ['testsOpen'],
  data() {
    return {
      isDark:false
    };
  },
  methods: {
    toggleDarkMode() {
      // TODO: implement me
      this.isDark = !this.isDark
      this.$emit('changeMode',this.isDark )
    },
    toggleTests() {
      this.$emit('toggle-tests');
    }    
  }
}
</script>