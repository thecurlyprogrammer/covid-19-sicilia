<template>
  <div class="main" id="bollettino">
    <div class="head">
      <div class="title">Coronavirus in {{ sicilia.regione }}</div>
      <div class="data">Bollettino aggiornato in data: {{ sicilia.data }}</div>
    </div>
    <b-container>
      <firstRow
        :ricoverati = "sicilia.ricoveratiSintomi"
        :terapia = "sicilia.terapiaIntensiva"
        :ospedalizzati = "sicilia.totaleOspedalizzati"
        :isolamento = "sicilia.isolamentoDomiciliare"
      />
      <secondRow
        :totalePositivi = "sicilia.totalePositivi"
        :nuoviPositivi = "sicilia.nuoviPositivi"
        :dimessi = "sicilia.dimessiGuariti"
        :deceduti = "sicilia.deceduti"
        :totaleCasi = "sicilia.totaleCasi"
        :tamponi = "sicilia.tamponi"
      />
      <province
        :province = "provinceTotale"
      />
      <nazione
        :ricoverati = "nazione.ricoveratiSintomi"
        :terapia = "nazione.terapiaIntensiva"
        :ospedalizzati = "nazione.totaleOspedalizzati"
        :isolamento = "nazione.isolamentoDomiciliare"
        :totalePositivi = "nazione.totalePositivi"
        :nuoviPositivi = "nazione.nuoviPositivi"
        :dimessi = "nazione.dimessiGuariti"
        :deceduti = "nazione.deceduti"
        :totaleCasi = "nazione.totaleCasi"
        :tamponi = "nazione.tamponi"
      />
      <hr>
      <b-row class="amazon">
        <iframe src="https://rcm-eu.amazon-adsystem.com/e/cm?o=29&p=13&l=ur1&category=amu&banner=0Y59GJHNAWRPWXVM5SR2&f=ifr&linkID=491b8e35c9d3d4c4913ce8f958de9b3b&t=sandrogreco0a-21&tracking_id=sandrogreco0a-21" width="468" height="60" scrolling="no" border="0" marginwidth="0" style="border:none;" frameborder="0"></iframe>
      </b-row>
      <hr>
      <div class="vamedecumContainer" id="cosaFare">
        <div class="vamedecum">Cosa fare in caso di dubbi?</div>
        <b-list-group>
          <b-list-group-item v-for="regola in regole" v-bind:key="regola.key">
            {{ regola }}
          </b-list-group-item>
        </b-list-group>
        <div class="credits">Fonte:
          <b-link href="http://www.salute.gov.it/imgs/C_17_opuscoliPoster_444_allegato.pdf" target="blank">
            www.salute.gov.it
          </b-link>
        </div>
      </div>
      <hr>
      <div class="rivolgersiContainer" id="contatti">
        <div class="rivolgersi">A chi rivolgersi?</div>
        <b-list-group>
          <b-list-group-item v-for="contatto in contatti" v-bind:key="contatto.key">
            {{ contatto.titolo }} , <b-link :href="contatto.link" target="blank">
              {{ contatto.placeholder }}
            </b-link>
          </b-list-group-item>
        </b-list-group>
      </div>
      <b-row class="amazon">
        <iframe src="https://rcm-eu.amazon-adsystem.com/e/cm?o=29&p=22&l=ur1&category=prime&banner=04NK6M6RAGQ5Q3BQ0282&f=ifr&linkID=e6b910429505fb4dde31e6f47d79afdd&t=sandrogreco0a-21&tracking_id=sandrogreco0a-21" width="250" height="250" scrolling="no" border="0" marginwidth="0" style="border:none;" frameborder="0"></iframe>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import axios from 'axios';
import firstRow from '@/components/firstRow.vue';
import secondRow from '@/components/secondRow.vue';
import province from '@/components/province.vue';
import nazione from '@/components/nazione.vue';

export default {
  name: 'Home',
  data() {
    return {
      sicilia: {
        regione: 'Sicilia',
        data: '2020-00-00',
        ricoveratiSintomi: '0',
        terapiaIntensiva: '0',
        totaleOspedalizzati: '0',
        isolamentoDomiciliare: '0',
        totalePositivi: '0',
        nuoviPositivi: '0',
        dimessiGuariti: '0',
        deceduti: '0',
        totaleCasi: '0',
        tamponi: '0',
      },
      nazione: {
        stato: 'Italia',
        ricoveratiSintomi: '0',
        terapiaIntensiva: '0',
        totaleOspedalizzati: '0',
        isolamentoDomiciliare: '0',
        totalePositivi: '0',
        nuoviPositivi: '0',
        dimessiGuariti: '0',
        deceduti: '0',
        totaleCasi: '0',
        tamponi: '0',
      },
      provinceTotale: [],
      regole: {
        1: '1. Quali sono i sintomi a cui devo fare attenzione? Febbre e sintomi simil-influenzali come tosse, mal di gola, respiro corto, dolore ai muscoli, stanchezza sono segnali di una possibile infezione da nuovo coronavirus.',
        2: '2. Ho febbre e/o sintomi influenzali, cosa devo fare? Resta in casa e chiama il medico di famiglia, il pediatra o la guardia medica.',
        3: '3. Dopo quanto tempo devo chiamare il medico? Subito. Se ritieni di essere contagiato, chiama appena avverti i sintomi di infezione respiratoria, spiegando i sintomi e i contatti a rischio.',
        4: '4. Non riesco a contattare il mio medico di famiglia, cosa devo fare? Chiama uno dei numeri di emergenza indicati sul sito www.salute.gov.it/nuovocoronavirus',
        5: '5. Posso andare direttamente al pronto soccorso o dal mio medico di famiglia? No. Se accedi al pronto soccorso o vai in un ambulatorio senza prima averlo concordato con il medico potresti contagiare altre persone.',
        6: '6. Come posso proteggere i miei familiari? Segui sempre i comportamenti di igiene personale (lavati regolarmente le mani con acqua e sapone o usa un gel a base alcolica) e mantieni pulito l`ambiente. Se pensi di essere infetto indossa una mascherina chirurgica, resta a distanza dai tuoi familiari e disinfetta spesso gli oggetti di uso comune.',
        7: '7. Dove posso fare il test? I test vengono eseguiti unicamente in laboratori del Servizio Sanitario Nazionale selezionati. Se il tuo medico ritiene che sia necessario un test ti fornirà indicazioni su come procedere.',
        8: '8. Dove trovo altre informazioni attendibili? Segui solo le indicazioni specifiche e aggiornate dei siti web ufficiali, delle autorità locali e della Protezione Civile.',
      },
      contatti: [
        {
          titolo: 'Regione Sicilia',
          link: 'http://pti.regione.sicilia.it/portal/page/portal/PIR_PORTALE/',
          placeholder: 'Link al Sito Web',
        },
        {
          titolo: 'Numero Verde Regione Sicilia',
          link: 'tel:800 45 87 87',
          placeholder: '800 45 87 87',
        },
      ],
    };
  },
  regione: [],
  components: {
    firstRow,
    secondRow,
    province,
    nazione,
  },
  methods: {
    getRegione() {
      const path = 'https://raw.githubusercontent.com/pcm-dpc/COVID-19/master/dati-json/dpc-covid19-ita-regioni-latest.json';
      axios.get(path)
        .then((res) => {
          const result = res.data;
          const lunghezza = result.length;
          let i = 0;
          while (i < lunghezza) {
            if (result[i].codice_regione === 19) {
              this.sicilia.regione = res.data[i].denominazione_regione;
              this.sicilia.data = res.data[i].data;
              this.sicilia.ricoveratiSintomi = res.data[i].ricoverati_con_sintomi;
              this.sicilia.terapiaIntensiva = res.data[i].terapia_intensiva;
              this.sicilia.totaleOspedalizzati = res.data[i].totale_ospedalizzati;
              this.sicilia.isolamentoDomiciliare = res.data[i].isolamento_domiciliare;
              this.sicilia.totalePositivi = res.data[i].totale_attualmente_positivi;
              this.sicilia.nuoviPositivi = res.data[i].nuovi_attualmente_positivi;
              this.sicilia.dimessiGuariti = res.data[i].dimessi_guariti;
              this.sicilia.deceduti = res.data[i].deceduti;
              this.sicilia.totaleCasi = res.data[i].totale_casi;
              this.sicilia.tamponi = res.data[i].tamponi;
            }
            i += 1;
          }
        })
        .catch((error) => {
          // eslint-disable-next-line
          console.error(error);
        });
    },
    getProvince() {
      const path = 'https://raw.githubusercontent.com/pcm-dpc/COVID-19/master/dati-json/dpc-covid19-ita-province-latest.json';
      axios.get(path)
        .then((res) => {
          const result = res.data;
          const lunghezza = result.length;
          let i = 0;
          while (i < lunghezza) {
            if (result[i].codice_regione === 19) {
              if (result[i].denominazione_provincia !== 'In fase di definizione/aggiornamento') {
                this.provinceTotale.push(result[i]);
                // console.log(this.provinceTotale);
              }
            }
            i += 1;
          }
          // console.log(this.provinceTotale);
        })
        .catch((error) => {
          // eslint-disable-next-line
          console.error(error);
        });
    },
    getNazione() {
      const path = 'https://raw.githubusercontent.com/pcm-dpc/COVID-19/master/dati-json/dpc-covid19-ita-andamento-nazionale-latest.json';
      axios.get(path)
        .then((res) => {
          this.nazione.stato = res.data[0].stato;
          this.nazione.ricoveratiSintomi = res.data[0].ricoverati_con_sintomi;
          this.nazione.terapiaIntensiva = res.data[0].terapia_intensiva;
          this.nazione.totaleOspedalizzati = res.data[0].totale_ospedalizzati;
          this.nazione.isolamentoDomiciliare = res.data[0].isolamento_domiciliare;
          this.nazione.totalePositivi = res.data[0].totale_attualmente_positivi;
          this.nazione.nuoviPositivi = res.data[0].nuovi_attualmente_positivi;
          this.nazione.dimessiGuariti = res.data[0].dimessi_guariti;
          this.nazione.deceduti = res.data[0].deceduti;
          this.nazione.totaleCasi = res.data[0].totale_casi;
          this.nazione.tamponi = res.data[0].tamponi;
          // console.log(this.nazione);
        })
        .catch((error) => {
          // eslint-disable-next-line
          console.error(error);
        });
    },
  },
  created() {
    this.getRegione();
    this.getProvince();
    this.getNazione();
  },
};
</script>

<style lang="scss" scoped>
  #bollettino{
    margin-top: 100px;
  }
  .main{
    background-color: #f5f6fa;
    .widgetContainer{
      // background-color: blue;
      padding: 16px;
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
        height: 80px;
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
    .head{
      // background-color: aqua;
      padding: 16px;
      .title{
        font-size: 3em;
        text-align: center;
        font-family: 'Raleway', sans-serif;
        font-weight: 300;
      }
      .data{
        font-size: 1.3em;
        text-align: center;
        font-family: 'Raleway', sans-serif;
      }
    }
    .vamedecumContainer{
      .vamedecum{
        font-size: 2.5em;
        font-family: 'Raleway', sans-serif;
        font-weight: 300;
        text-align: center;
        padding: 16px 0px;
      }
      .credits{
        margin-top: 16px;
        text-align: center;
        font-family: 'Raleway', sans-serif;
      }
    }
    .rivolgersiContainer{
      padding: 16px 0px;
      .rivolgersi{
        font-size: 2.5em;
        text-align: center;
        font-family: 'Raleway', sans-serif;
        font-weight: 300;
        padding: 16px 0px;
      }
    }
    .amazon{
      display: flex;
      justify-content: center;
      padding: 16px;
      .amazonProduct{
        margin-bottom: 16px;
      }
    }
  }
</style>
