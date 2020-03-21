<template>
  <div>
    <hr>
    <b-row>
      <b-col class="widgetContainer" lg="3" md="6" sm="6" cols="6">
        <div class="iconContainer">
          <img class="icons" src="../assets/icons/01.svg"
          alt="Icona che raffigura una persona che tossisce">
        </div>
        <div class="title">Ricoverati con Sintomi</div>
        <div class="value">{{ ricoverati }}</div>
      </b-col>
      <b-col class="widgetContainer" lg="3" md="6" sm="6" cols="6">
        <div class="iconContainer">
          <img class="icons" src="../assets/icons/02.svg"
          alt="Icona che raffigura dei polmoni">
        </div>
        <div class="title">Terapia Intensiva</div>
        <div class="value">{{ terapia }}</div>
      </b-col>
      <b-col class="widgetContainer" lg="3" md="6" sm="6" cols="6">
        <div class="iconContainer">
          <img class="icons" src="../assets/icons/03.svg"
          alt="Icona che raffigura un ospedale">
        </div>
        <div class="title">Totale Ospedalizzati</div>
        <div class="value">{{ ospedalizzati }}</div>
      </b-col>
      <b-col class="widgetContainer" lg="3" md="6" sm="6" cols="6">
        <div class="iconContainer">
          <img class="icons" src="../assets/icons/04.svg"
          alt="Icona che raffigura un paziente con una mascherina">
        </div>
        <div class="title">Isolamento Domiciliare</div>
        <div class="value">{{ isolamento }}</div>
      </b-col>
    </b-row>
  </div>
</template>

<script>

export default {
  name: 'Home',
  props: ['ricoverati', 'terapia', 'ospedalizzati', 'isolamento'],
  data() {
    return {
    };
  },
};
</script>

<style lang="scss" scoped>
  .main{
.widgetContainer{
      // background-color: blue;
      padding: 16px;
      // margin-bottom: 16px;
      .iconContainer{
        width: 100%;
        // background-color: green;
        display: flex;
        justify-content: center;
        margin-bottom: 16px;
      }
      .icons{
        // background-color: red;
        width: auto;
        height: 120px;
      }
      .title{
        font-size: 1.2em;
        text-align: center;
      }
      .value{
        font-size: 3em;
        text-align: center;
      }
    }
  }
</style>
