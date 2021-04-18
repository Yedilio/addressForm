<template>
  <div id="app">
    <AddressForm />
  </div>
</template>

<script>
  import AddressForm from "./components/AddressForm";
  // import ModalWindows from "./components/ModalWindows";

  export default {
    name: 'App',
    components: {
      AddressForm,
      // ModalWindows
    }
  }
</script>

<style lang="scss" scoped>
  div {
    height: 100%;
    width: 100%;
    background-color: rgba(34, 34, 34, .9);
    display: flex;
    justify-content: center;
  }
</style>
