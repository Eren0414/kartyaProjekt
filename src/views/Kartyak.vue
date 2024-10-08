<template>
  <h2>Karakter kártyák</h2>
  <!-- Kártyák -->
  <div class="row row-cols-1 row-cols-md-3 row-cols-lg-4 g-4 karakter-kartyak">
    <KarakterKartya
      v-for="karakter in szurtKarakterek"
      :key="karakter.id"
      :id="karakter.id"
      @karaterModalReszletKezeles="reszletModalKezelo"
      class="karakter-kartya"
    >
      <!-- V-slots -->
      <template v-slot:kep>
        <img :src="karakter.kep" :alt="karakter.cim" class="karakter-kep" />
      </template>
      <template v-slot:cim>
        <p v-html="keresJelol(karakter.cim)" class="karakter-cim"></p>
      </template>
    </KarakterKartya>
  </div>
  <div v-if="szurtKarakterek.length == 0">Nincs találat</div>

  <!-- Kartyainfo Modal -->
  <KartyaInfo :cim="keresJelol(kivalasztottKarakter.cim)">
    <img
      :src="kivalasztottKarakter.kep"
      :alt="kivalasztottKarakter.cim"
      class="float-start col-12 col-sm-6 col-lg-4 me-1 p-2 my-picture"
    />
    <div v-html="keresJelol(szovegFormatum)"></div>
  </KartyaInfo>
</template>

<script>
class Karakter {
  constructor(id = 0, cim = null, kep = null, szoveg = null) {
    this.id = id;
    this.cim = cim;
    this.kep = kep;
    this.szoveg = szoveg;
  }
}
import KarakterKartya from "@/components/KarakterKartya.vue";
import KartyaInfo from "@/components/KartyaInfo.vue";
export default {
  components: {
    KarakterKartya,
    KartyaInfo,
  },
  inject: ["keresoSzo"],
  data() {
    return {
      kivalasztottKarakter: new Karakter(),
      karakterek: [
        {
          id: 1,
          cim: "Alucard",
          kep: "alucard.png",
          szoveg: [
            "Alucard a Kohta Hirano által készített Hellsing- sorozat három főszereplőjének egyike Sir Integra és Seras Victoria mellett.",
            "A Hellsing mindkét adaptációjábana japán szubban Jouji Nakata , az angol szinkronban pedig Crispin Freeman ad hangot",
            "többször is, amíg nem kap határozott választ. Azt sugallják, hogy ő a legerősebb vámpír az életben, és a legerősebb karakter a sorozatban.",
          ],
        },
        {
          id: 2,
          cim: "Anderson",
          kep: "anderson.png",
          szoveg: [
            "Seras Victoria egyike a Kohta Hirano által alkotott Hellsing- sorozat három főszereplőjének, Alucard és Sir Integra mellett.",
            "A Hellsing mindkét adaptációjában a japán szubban Fumiko Orikasa ,az angol szinkronban pedig KT Gray ad hangot",
            "Serast Alucard vámpírrá változtatta, hogy megmentse őt egy esetleges halálos lövéstől a mellkasában, amelyet a Pásztor lövése közben is okozott.",
            "Ettől kezdve segíti a Hellsing Organizationt a megnövekedett vámpírtámadások ellen, majd később Sir Integra közeli munkatársa lesz, és romantikus kapcsolatot alakít ki Pip Vernedeaddel. Seras egy Drakulina, ez a kifejezés a Dracul vérvonal női tagjaira utal, mióta Alucard vámpírrá változtatta.",
          ],
        },
        {
          id: 3,
          cim: "Captain",
          kep: "captain.png",
          szoveg: [
            "A kapitány a Kohta Hirano által létrehozott Hellsing sorozat egyik fő antagonistája.",
            "Nincs beszélő szerepe az OVA egészében, és nincs párbeszéde a mangában sem.",
            "A kapitány az őrnagy néma, sztoikus adjutánsa és testőre; kiáll az őrnagy kívánságainak, aki egyik legjobb jobbkeze és mindig hűséges testőre.",
            "A kapitány egy természetes vérfarkas, aki tetszés szerint képes átalakulni és harcolni akár emberi, akár vérfarkas alakban.",
            "Ahogy Alucard Hellsing ütőkártyája, Alexander Anderson pedig Iscarioté, úgy a kapitány volt a Millenium ütőkártyája.",
          ],
        },
        {
          id: 4,
          cim: "Dornez",
          kep: "dornez.png",
          szoveg: [
            "A Hellsing Family Butler Walter C. Dornez, Worutā Kumu Dorunēzu Herushingu-ka batorā, OVA : Walter C. Dollneaz 》a Kohta Hirano által létrehozott Hellsing- sorozat egyik fő mellékszereplője, aki fő antagonistává vált.",
            "A Hellsing mindkét adaptációjábana japán szubban Motomu Kiyokawa, az angol szinkronban pedig Ralph Lister ad hangot.",
            "Daisuke Namikawa és Liam O' Brien a fiatal felnőtt Waltert, míg Romi Park és Jessica D. Stone a legfiatalabb változatát.",
            "Noha Integra Hellsing komornyikjaként szolgált, halálos borotvaéles drótokkal még mindig bebizonyította, hogy megfelel a „Halál angyala” becenevének.",
            "Szoros barátság fűzte az Integrához és a Hellsing Organization Trump Card, Alucardhoz is. Korábban a Hellsing Organization aktív tagja volt, és a család megtartójaként dolgozott, amíg el nem árulta őket a Milleniumra.",
          ],
        },
        {
          id: 5,
          cim: "Major",
          kep: "major.png",
          szoveg: [
            "Nincs elérhető leírás ennél a karakterről."
        ],
        },
        {
          id: 7,
          cim: "Schrodinger",
          kep: "schrodinger.png",
          szoveg: [
            "Nincs elérhető leírás ennél a karakterről."
        ],
        },
        {
          id: 8,
          cim: "Victoria",
          kep: "victoria.png",
          szoveg: [
            "Nincs elérhető leírás ennél a karakterről."
        ],
        },
        {
          id: 9,
          cim: "Wingates",
          kep: "wingates.png",
          szoveg: [
            "Nincs elérhető leírás ennél a karakterről."
        ],
        },
      ],
    };
  },
  methods: {
    reszletModalKezelo(id) {
      this.kivalasztottKarakter = this.karakterek.filter((k) => k.id == id.id)[0];
    },
    keresJelol(szoveg) {
      if (this.keresoSzo) {
        let what = new RegExp(this.keresoSzo, "gi");
        if (szoveg) {
          szoveg = szoveg.replace(what, (match) => {
            return `<span class="mark p-0">${match}</span>`;
          });
        }
        return szoveg;
      } else {
        return szoveg;
      }
    },
  },
  computed: {
    szovegFormatum() {
      if (this.kivalasztottKarakter.szoveg == null) {
        return `<p></p>`;
      }
      return this.kivalasztottKarakter.szoveg
        .map((k) => `<p>${k}</p>`)
        .join("");
    },
    szurtKarakterek() {
      if (!this.keresoSzo) {
        return this.karakterek;
      }
      return this.karakterek.filter(k => {
        return k.cim.toLowerCase().includes(this.keresoSzo.toLowerCase()) ||
        k.szoveg.some(k => k.toLowerCase().includes(this.keresoSzo.toLowerCase()))
      });
    },
  },
};
</script>

<style scoped>
.karakter-kartyak {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
}

.karakter-kartya {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
  border: 1px solid #ddd;
  border-radius: 8px;
  padding: 15px;
  background-color: #f9f9f9;
  height: 100%;
}

.karakter-kartya img {
  max-width: 100%;
  height: auto;
  object-fit: cover;
}

.karakter-kep {
  width: 100%;
  height: 150px; 
  object-fit: cover;
  border-radius: 8px;
}

.karakter-cim {
  font-weight: bold;
  text-align: center;
  margin-top: 10px;
}

.row-cols-1 .karakter-kartya {
  margin-bottom: 20px;
}

@media (min-width: 768px) {
  .row-cols-md-3 .karakter-kartya {
    flex-basis: calc(33.3333% - 20px); 
    margin-bottom: 20px;
  }
}

@media (min-width: 992px) {
  .row-cols-lg-4 .karakter-kartya {
    flex-basis: calc(25% - 20px); 
    margin-bottom: 20px;
  }
}
</style>