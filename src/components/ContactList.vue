<script setup>
import useContactList from "./composables/useContactList";
import ContacCard from "./ContacCard.vue";
import ContacFilter from "./ContacFilter.vue";
import Spinner from "../utils/Spinner.vue";

const { contacts, state } = useContactList();
</script>

<template>
  <div
    v-if="state.loading"
    class="d-flex justify-content-center align-items-center"
  >
    <Spinner />
  </div>
  <div v-else>
    <ContacFilter v-if="contacts.length > 0" />
    <transition name="switch" mode="out-in" appear>
      <div v-if="contacts.length > 0">
        <transition-group name="list" appear>
          <div v-for="contact in contacts" :key="contact?.id">
            <ContacCard :contact="contact" />
          </div>
        </transition-group>
      </div>
    </transition>
  </div>
</template>

<style scoped>
/* switch transitions */
.switch-enter-from,
.switch-leave-to {
  opacity: 0;
  transform: translateY(20px);
}
.switch-enter-active,
.switch-leave-active {
  transition: all 0.5s ease;
}
</style>
