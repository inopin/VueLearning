<template>
  <li>
    <h2>{{ name }} {{ isFavorite ? '(Favorite)' : '' }}</h2>
    <button @click="toggleFavorite"> toggle Favorite</button>
    <button @click="toggleDetails">{{ detailsAreVisible ? 'Hide' : 'Show' }} Details</button>
    <ul v-if="detailsAreVisible">
      <li>
        <strong>Phone:</strong>
        {{ phoneNumber }}
      </li>
      <li>
        <strong>Email:</strong>
        {{ emailAdress }}
      </li>
    </ul>
    <button @click="deleteFriend">Delete</button>
  </li>
</template>

<script>
export default {
  // props:['name', 'phoneNumber', 'emailAdress', 'isFavorite'],
  props:{
    id:{
      type: String,
      required: true,
    },
    name: {
      type: String,
      required: true},

    phoneNumber:{
     type: String,
     required: true
    },
    emailAdress: {
      type: String,
      required: true
    },
    isFavorite: {
      type: Boolean,
      required:false,
      default:false,
    },
  },
  emits: ['toggle-favorite','delete-friend'],
  data() {
    return {
      detailsAreVisible: false,
    };
  },
  methods: {
    toggleDetails() {
      this.detailsAreVisible = !this.detailsAreVisible;
    },
    toggleFavorite() {
      this.$emit('toggle-favorite', this.id)
    },
    deleteFriend() {
      this.$emit('delete-friend', this.id)
    }
  }
};
</script>