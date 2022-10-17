<script setup>
import { toRef } from "vue";
import { useContectStore } from "../stores/contact.store";

const props = defineProps(["contact"]);
const contact = toRef(props, "contact");
const contactStore = useContectStore();
const { deleteContact, setCurrentContact } = contactStore;
</script>

<template>
  <div
    class="modal fade"
    id="confirmDelete"
    tabindex="-1"
    aria-labelledby="confirmDeleteLabel"
    aria-hidden="true"
  >
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title" id="confirmDeleteLabel">Alert!</h5>
          <button
            type="button"
            class="btn-close"
            data-bs-dismiss="modal"
            aria-label="Close"
          ></button>
        </div>
        <div class="modal-body">Are You sure want to delete this Contact?</div>
        <div class="modal-footer">
          <button class="btn btn-secondary" data-bs-dismiss="modal">
            Cancel
          </button>
          <button
            class="btn btn-danger"
            data-bs-dismiss="modal"
            @click="deleteContact(contact.id)"
          >
            Delete
          </button>
        </div>
      </div>
    </div>
  </div>

  <div class="w-100 pt-2">
    <div class="card shadow border-0">
      <div class="card-header d-flex justify-content-between">
        <span v-if="contact.name" class="fw-bold">{{ contact.name }}</span>
        <span
          v-if="contact.type"
          class="badge text-capitalize"
          :class="[
            contact.type === 'Professional'
              ? 'bg-warning text-dark'
              : 'bg-danger ',
          ]"
        >
          {{ contact.type }}
        </span>
      </div>
      <div class="card-body">
        <div class="card-text">
          <div v-if="contact.email">
            <i class="fas fa-envelope-open text-info me-3" />
            {{ contact.email }}
          </div>
          <div v-if="contact.phone">
            <i class="fas fa-phone text-info me-3" />
            {{ contact.phone }}
          </div>
        </div>
        <hr />
        <div class="d-flex justify-content-between">
          <button
            class="btn btn-dark"
            @click="setCurrentContact(props.contact)"
          >
            Edit
          </button>
          <button
            class="btn btn-danger"
            data-bs-toggle="modal"
            data-bs-target="#confirmDelete"
          >
            Delete
          </button>
        </div>
      </div>
    </div>
  </div>
</template>
