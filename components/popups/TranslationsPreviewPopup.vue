<template>
  <PopupContainer v-if="visible" @close="visible = false" :full-height="true">
    <h3 class="text-lg font-bold text-center mb-4">Alle Übersetzungen</h3>
    <div class="h-px w-20 mx-auto bg-accent mb-4" />
    <table>
      <tr v-for="(translation, id) in translations" v-bind:key="id" class="my-2">

        <!-- Desktop -->
        <td class="font-bold p-2 hidden sm:table-cell">{{translation.term}}</td>
        <td class="p-2 hidden sm:table-cell">
          <span class="whitespace-no-wrap">
            ... wird zu ...
          </span>
        </td>
        <td class="font-bold p-2 hidden sm:table-cell">{{translation.replaceString}}</td>

        <!-- Mobile -->
        <td class="py-2 md:hidden">
          {{translation.term}} <br>
          <font-awesome-icon icon="arrow-right" size="sm" class="mx-1"/>{{translation.replaceString}}
        </td>

      </tr>
    </table>

  </PopupContainer>
</template>
<script>
  import PopupContainer from "../gui-elements/PopupContainer";

  export default {
    components: {PopupContainer},
    data() {
      return {
        visible: false
      }
    },
    methods: {
      show() {
        this.visible = true;
      }
    },
    computed: {
      translations () {
        return this.$store.state.terms.terms.sort((a, b) => {
          if (a.term.toUpperCase() < b.term.toUpperCase())
            return -1;
          else
            return 1;

        }).filter((val) => val.term !== "");
      }
    }
  }
</script>
