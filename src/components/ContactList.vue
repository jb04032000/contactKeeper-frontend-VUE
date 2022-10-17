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
    <ContacFilter v-if="contacts.length" />
    <transition name="switch" mode="out-in">
      <div>
        <transition-group name="list" appear>
          <div v-if="contacts">
            <ContacCard
              v-for="contact in contacts"
              :key="contact?.id"
              :contact="contact"
            />
          </div>
        </transition-group>
      </div>
    </transition>
  </div>
</template>

<style scoped>
/* list transitions */
.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: scale(0.6);
}
.list-enter-to,
.list-leave-from {
  opacity: 1;
  transform: scale(1);
}
.list-enter-active {
  transition: all 0.4s ease;
}
.list-leave-active {
  transition: all 0.4s ease;
  position: absolute;
}

.list-move {
  transition: all 0.3s ease;
}

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
