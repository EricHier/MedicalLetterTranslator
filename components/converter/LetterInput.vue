<template>
  <div class="px-8 py-10 w-full">
    <div class="container mx-auto">
      <div class="md:flex justify-center items-center w-full subpixel-antialiased">
        <div class="md:w-1/2 md:p-5 md:pl-0 mb-8">
          <p class="text-lg font-700">
            Hier kannst du deinen <strong>Arztbrief eingeben</strong>. Dieser wird dann
            <strong>automatisch von unserem Algorithmus gescannt</strong> und
            analysiert. Dafür greifen wir auf die Datenbank mit <strong>mehreren hundert Begriffen</strong> zu.
          </p>
          <div class="h-px w-12 mt-4 bg-accent"/>
          <button @click="setExample" class="outline-none p-2 border border-focus w-fit text-accent font-bold mt-4">
            {{ input ? "» Textfeld leeren" : "» Beispieltext einfügen" }}
          </button>
        </div>
        <div class="md:p-5 md:pr-0 md:w-1/2">
          <textarea v-model="input" @keyup="keyup"
                    class="w-full border shadow-xl text-blue focus:text-accent focus:border-focus h-64 rounded-sm  p-4 outline-none"
                    placeholder="Eingabe"/>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      input: ""
    }
  },
  methods: {
    async keyup(e) {
      const _ = await import("lodash"), input = e.target.value;

      this.$store.commit("setShown", !!input);
      this.$store.commit("setLoading", !!input);

      if (input) {
        _.debounce((input) => {
          this.$store.commit("setInput", input);
          this.$store.commit("setLoading", false);
        }, 2500)(input);
      }
    },
    setExample() {
      this.input = this.input ? "" : "Bei Eintreffen des Notarztes gibt die Patientin seit einigen Tagen bestehende  Hämatochezie an. Eine ÖGD oder Koloskopie wurden bis dato noch nie durchgeführt. Übelkeit, Erbrechen, Fieber, Nachtschweiss, Gewichtsverlust, Dyspnoe wurden verneint.";
      this.keyup({
        target: {
          value: this.input
        }
      });
    }
  }
}
</script>
<style>
.outline-none {
  outline-width: 0;
  outline-style: none;
  outline: none;
}
</style>
