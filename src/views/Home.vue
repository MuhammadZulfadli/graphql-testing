<template>
  <div>
    <nomination-board />
  </div>
</template>

<script>
// @ is an alias to /src
import NominationBoard from "@/components/NominationBoard.vue";
// import NominationModal from "../components/NominationModal.vue";

export default {
  name: "Home",
  components: {
    NominationBoard
  }
};
</script>
