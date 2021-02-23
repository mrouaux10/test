<template>
  <div class="home">
    <b-container>
      <b-row align-h="center">
        <h2 class="title">Lista de Usuarios</h2>
      </b-row>
    </b-container>
    <b-container>
      <b-row class="justify-content-around">
        <h6>Cuentas bloqueadassssssss: {{ blockedAccounts.length }}</h6>
        <h6>Cuentas activas: {{ activeAccounts.length }}</h6>
      </b-row>
      <b-row class="justify-content-around">
        <h6>Hay menores de edad? {{ youngers ? 'Sí' : 'No' }}</h6>
        <h6>Promedio de edades de adultos {{ adultsAVG.toFixed(3) }}</h6>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import Users from '../users/users.json';
export default {
  name: "Home",
  components: {},
  data() {
    return {
      usersData: {},
      blockedAccounts: 0,
      activeAccounts: 0,
      youngers: null,
      adults: 0

    }
  },
  mounted() {
    this.getUsersInfo();
  },
  methods: {
    getUsersInfo() {
      this.usersData = Users.data.users;
      this.blockedAccounts = this.usersData.filter(user => user.status === 2);
      this.activeAccounts  = this.usersData.filter(user => user.status === 1);
      this.youngers = this.usersData.find(user => user.age < 18);
      this.adults = this.usersData.filter(user => user.age >= 18);
      this.adultsAges = this.adults.map((adult) => adult.age).reduce((previous, current) => current += previous);
      this.adultsAVG = this.adultsAges / this.adults.length;
    }
  }
};
</script>

<style lang="scss">
.home {
  .title {
    margin-top: 2rem;
  }
}
</style>