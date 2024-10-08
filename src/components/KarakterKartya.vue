<template>
  <div class="col">
    <div class="card">
      <slot name="kep"></slot>
      <div class="card-body">
        <slot name="cim"></slot>
        <button type="button" class="btn btn-danger" data-bs-toggle="modal" data-bs-target="#karakterInfoModal"
          @click="onClickReszletek()">
          Részletek
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["id"],
  methods: {
    onClickReszletek() {
      this.$emit("karaterModalReszletKezeles", { id: this.id });
    },
  },
}
</script>

<style></style>