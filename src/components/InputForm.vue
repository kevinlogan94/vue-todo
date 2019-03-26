<template>       
    <form>
        <input :disabled="editable" class="spacing-s--bottom-alt" v-model="inputValue" required/>
        <button :disabled="editable"  class="spacing-s--bottom-alt" type="submit" v-on:click="submitForm">Submit</button>
        <p class="error" v-if="error">{{error}}</p>
    </form>
</template>

<script>
export default {
  name: 'InputForm',
  data: function() {
    return {
        inputValue: "",
        error: ""
    }
  },
  methods: {
    submitForm: function(e) {
        //Prevents the form from reloading the page. 
        e.preventDefault();

        if(this.inputValue) {
            this.error = "";
            this.submit(this.inputValue);
            this.inputValue = "";
        } else {
            this.error = this.errorMessage;
        }
    }
  },
  props: {
    editable: Boolean,
    errorMessage: String,
    submit: Function
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    .error {
        color: red;
        font-size: 12px;
        padding-top: 0;
        margin-top: 2px;
    }
</style>
