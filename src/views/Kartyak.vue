<template>
  <!-- Kártyák -->
  <div class="row row-cols-1 row-cols-md-3 row-cols-lg-4 g-4 karakter-kartyak">
    <KarakterKartya v-for="karakter in szurtKarakterek" :key="karakter.id" :id="karakter.id"
      @karaterModalReszletKezeles="reszletModalKezelo" class="karakter-kartya">
      <!-- V-slots -->
      <template v-slot:kep>
        <img :src="karakter.kep" :alt="karakter.cim" class="karakter-kep" />
      </template>
      <template v-slot:cim>
        <p v-html="keresJelol(karakter.cim)" class="karakter-cim"></p>
      </template>
    </KarakterKartya>
  </div>
  <div v-if="szurtKarakterek.length == 0" class="null">Nincs találat</div>

  <!-- Kartyainfo Modal -->
  <KartyaInfo :cim="keresJelol(kivalasztottKarakter.cim)">
    <img :src="kivalasztottKarakter.kep" :alt="kivalasztottKarakter.cim"
      class="float-start col-12 col-sm-6 col-lg-4 me-1 p-2 my-picture" />
    <div v-html="keresJelol(szovegFormatum)"></div>
  </KartyaInfo>
</template>

<script>
// Karakter osztály
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
            "SS Sturmbannführer Montina Max, amelyet inkább The címe ismert Őrnagy, a Hellsing által létrehozott sorozat Kohta Hirano. Ő hangolja Nobuo Tobita japánul és Gildart Jackson az angol dub-ban.",
            "Az SS volt hadnagya, Adolf Hitler kiadott egy speciális parancsot (# 666), amely egy szigorúan titkos projekt felelősségére helyezte őt, amelynek fő hangsúlya a mesterséges vámpírizációs folyamat tökéletesítése volt.",
          ],
        },
        {
          id: 7,
          cim: "Schrodinger",
          kep: "schrodinger.png",
          szoveg: [
            "Tisztviselő Schrödinger jelentős antagonista a Hellsing által létrehozott sorozat Kohta Hirano. Hangzott Ryoko Shiraishi a japán alcsoportban és Laura Bailey az angol dub-ban.",
            "Schrödinger a hadtiszt tisztségét töltötte be és a Millennium katonai egység A Werwolf Squad. Ő egy spritált, gyors szellemes és éles nyelvű wacat, akinek kiemelkedő füle elárulja démoni természetét. Ő szolgál Az őrnagy vitathatatlanul, és gyakran a gonosz büntetés fogadó végén van.",
            "Schrödinger természete örökké mindenhol és sehol, lényegében lehetővé teszi, hogy bárhol megjelenhessen, akár a saját elméjében is."
          ],
        },
        {
          id: 8,
          cim: "Victoria",
          kep: "victoria.png",
          szoveg: [
            "Seras Victoria egyike a Hellsing által létrehozott sorozat Kohta Hirano, mellett Alucard és Sir Integra. Mindkét adaptációban Hellsing, ő hangolja Fumiko Orikasa a japán alcsoportban és K. Szürke az angol dub-ban.",
            "Seras lett a vámpír által Alucard hogy megmentse őt a mellkasban levő halálos lövésektől, amelyeket ő is okozott a lelkész.",
            "Ettől a ponttól kezdve segíti a Hellsing szervezet a megnövekedett vámpír támadások ellen, és később közeli társává válik Sir Integra és romantikus kapcsolatot alakít ki Pip Vernedead.",
            "Seras egy Draculina, egy olyan kifejezés, amely a Dracul vérvonal női tagjaira utal, mivel Alucard vámpírrá változtatta."
          ],
        },
        {
          id: 9,
          cim: "Wingates",
          kep: "wingates.png",
          szoveg: [
            "Uram Integrált Fairbrook Wingates Hellsing, Integuraru Faruburuke Wingētsu Herushingu-Kyō, egyike a Hellsing által létrehozott sorozat Kohta Hirano, mellett Alucard és Seras Victoria.",
            "Hellsing mindkét adaptációjában hangot ad neki Yoshiko Sakakibara a japán alcsoportban és Victoria Harwood az angol dub - ban.Kaori Mizuhashi és Tricia Dicksonjapánul, illetve angolul adták hangjukat fiatalabb iterációjához, amely visszacsatolásokban jelent meg.",
            "A protestáns lovagok 22 éves nemesi tagja, aki a Hellsing család vezetője és utolsó tagja; leszármazottja Helsing professzor, a Hellsing szervezet, és Hellsing vámpírjának jelenlegi mestere, Alucard.",
            "Karizmával és hazafisággal vezeti a Hellsing Szervezetet, és egyike azon kevés embernek, aki képes ellenállni Alucard személyiségének erőinek és parancsolni tiszteletét."
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

<style scope>
::-webkit-scrollbar {
  display: none;
}

.karakter-kartyak {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  padding: 10px;
  gap: 15px;
}

.karakter-kartya {
  background: #2c2c2c;
  border: 1px solid #444;
  border-radius: 10px;
  box-shadow: 0px 6px 12px rgba(0, 0, 0, 0.5);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  position: relative;
  overflow: hidden;
  /* Kártyák szélessége */
}

.karakter-kartya:hover {
  transform: translateY(-8px);
  box-shadow: 0px 10px 20px rgba(255, 0, 0, 0.3);
  cursor: url('/cursor.png'), auto;
}

@media (max-width: 768px) {
  .karakter-kartyak {
    grid-template-columns: 1fr;
    gap: 20px;
  }
}

.karakter-kep {
  width: 100%;
  height: auto;
  max-height: 300px;
  object-fit: cover;
  filter: brightness(0.7);
  border-radius: 8px;
  transition: filter 0.3s;
}

.karakter-kartya:hover .karakter-kep {
  filter: brightness(1);
}

.karakter-cim {
  margin-top: 10px;
  font-weight: 700;
  font-size: 20px;
  font-family: 'Cinzel', serif;
  letter-spacing: 1px;
  text-transform: uppercase;
}

.karakter-kartyak {
  font-size: 16px;
  font-weight: bold;
  color: #ff6347;
  margin-top: 20px;
}

/* Hozzáadás sötétebb háttér és vérhatás a kiemeléshez */
span.mark {
  background-color: rgba(255, 0, 0, 0.3);
  color: #fff;
  padding: 2px 4px;
}

/* Fényhatás hozzáadása */
.karakter-kartya::after {
  content: '';
  position: absolute;
  top: 50%;
  left: 50%;
  width: 200%;
  height: 200%;
  background: radial-gradient(circle, rgba(255, 0, 0, 0.2) 0%, rgba(0, 0, 0, 0) 70%);
  transform: translate(-50%, -50%);
  opacity: 0;
  transition: opacity 0.3s ease;
}

.karakter-kartya:hover::after {
  opacity: 1;
}

/* Vércsepp háttér a kártya alatt */
.karakter-kartya::after {
  content: '';
  position: absolute;
  bottom: -30px;
  /* Az alaphelyzet a kártya alatt */
  left: 50%;
  width: 30px;
  height: 30px;
  border-radius: 50%;
}

.null {
  text-align: center;
  color: red;
  font-family: 'Old English Text MT', serif;
  font-size: 30px;
}
</style>
