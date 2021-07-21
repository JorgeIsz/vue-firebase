<template>
  <div class="default-layout">
    <header-partial></header-partial>
    <section class="section__hero py-6 bg-black bg-cover bg-center">
      <div class="container">
        <div class="section__form bg-white p-4 w-1/2 shadow-md">
          <h1 class="mb-2 text-4xl font-light text-grey-darkest">Find homes on Platzi Rooms</h1>
          <h2 class="mb-6 text-base text-grey-dark font-normal">
            Discover entire homes and private rooms perfect for any trip.
          </h2>
          <form class="form__search">
            <div class="mb-4">
              <label class="input__label" for="where">Where</label>
              <div class="form__field relative">
                <i class="input-icon material-icons absolute text-grey-darker">search</i>
                <input
                  class="input__search"
                  id="where"
                  type="text"
                  placeholder="Mexico City, Mexico"
                />
              </div>
            </div>
            <button
              class="px-2 py-4 bg-yellow-dark font-semibold w-full rounded text-yellow-darker"
            >
              Search
            </button>
          </form>
        </div>
      </div>
    </section>
    <main class="main">
      <slot></slot>
    </main>
    <footer-partial></footer-partial>
    <!-- Modals -->
    <modal :show="modals.login" @close-modal="closeModal('login')">
      <h2 class="text-gray text-center mb-6">Login</h2>
      <form class="flex flex-col">
        <label for="email" class="form__label">Email</label>
        <input type="text" placeholder="adamsandler@example.com" class="form__input">
        <label for="email" class="form__label">Password</label>
        <input type="password" placeholder="*********" class="form__input">
        <input type="submit" value="Login" class="font-bold p-3 mt-5 bg-teal text-white rounded">
      </form>
    </modal>
    <modal :show="modals.signup" @close-modal="closeModal('signup')">
      <h2 class="text-gray text-center mb-6">Sign up</h2>
      <form class="flex flex-col">
        <label for="email" class="form__label">Name</label>
        <input type="text" placeholder="Adam Sandler" class="form__input">
        <label for="email" class="form__label">Email</label>
        <input type="text" placeholder="adamsandler@example.com" class="form__input">
        <label for="email" class="form__label">Password</label>
        <input type="password" placeholder="*********" class="form__input">
        <input type="submit" value="Sign up" class="font-bold p-3 mt-5 bg-teal text-white rounded">
      </form>
    </modal>
  </div>
</template>

<script>
import HeaderPartial from '@/partials/HeaderPartial.vue';
import FooterPartial from '@/partials/FooterPartial.vue';
import Modal from '@/components/Modal.vue';
import { mapGetters } from 'vuex';

export default {
  name: 'DefaultLayout',
  components: {
    HeaderPartial,
    FooterPartial,
    Modal,
  },
  computed: {
    ...mapGetters(['modals']),
  },
  methods: {
    closeModal(name) {
      this.$store.dispatch('TOGGLE_MODAL_STATE', {
        name,
        value: false,
      });
    },
  },
};
</script>

<style>
.section__hero {
  min-height: 450px;
  background-image: url('https://images.unsplash.com/photo-1504202302068-15fc2055f7f9?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1330&q=80');
}

.form__label {
  margin: 10px 0;
  font-weight: bold;
}

.form__input {
  border: 1px solid gray;
  border-radius: 6px;
  padding: 10px;
}
.form__field .input-icon {
  top: 7px;
  left: 9px;
}

.form__field > .input__search {
  @apply pl-10;
}

@media (max-width: 576px) {
  .section__hero {
    min-height: 250px;
  }

  .section__form {
    @apply w-full;
  }
}
</style>
