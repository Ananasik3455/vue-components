<template>
  <v-menu
    v-model="menu"
    :close-on-content-click="false"
    
    transition="scale-transition"
    min-width="300"
    ref="menu"
    offset-y
    @
  >
    <template #activator="{ on }">
      <v-text-field
        v-model="time"
        append-icon="query_builder"
        label="Выбор времени"
        readonly
        v-on="on"
      />
    </template>

    <v-time-picker
      v-if="menu"
      v-model="time"
      format="24hr"
      locale="ru"
      use-seconds
      full-width
      @click:second="$refs.menu.save(time)"
    />
  </v-menu>
</template>

<script>
export default {
  name: 'TimeInput',

  props: {
    value: String,
  },

  data: () => ({
    menu: false,
  }),

  computed: {
    time: {
      get() {
        return this.value;
      },
      set(time) {
        this.$emit('input', time);
      },
    },
  },

  watch: {
    menu(menu) {
      if (!menu) {
        this.$refs.menu.save(this.time);
      }
    },
  },
};
</script>
