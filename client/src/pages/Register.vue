<template>
  <q-page class="flex flex-center">
    <div class="q-pa-md row items-start q-gutter-md">
    <q-card class="my-card">
      <q-card-section>
        <q-input v-model="text" label="Логин" />
        <br>
        <q-input v-model="text" label="Пароль" />
        <br>
        <q-btn color="secondary" class="full-width" label="Зарегистрироваться" />
      </q-card-section>
    </q-card>
    </div>
  </q-page>
</template>

<script>
export default {
  name: 'PageRegister',
  data() {
    return {
      text: null,
    };
  },
};
</script>
