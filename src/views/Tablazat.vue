<template>
    <div class="container-fluid">
        <div class="row justify-content-center align-items-start">
            <!-- Táblázat a karakterekről -->
            <div class="col-12 col-md-5 mb-4">
                <table class="table table-dark table-hover">
                    <thead>
                        <tr>
                            <th scope="col">Név</th>
                            <th scope="col">Hovatartozás</th>
                            <th scope="col">Becenév</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="karakter in filteredKarakterek" :key="karakter.id" @click="selectKarakter(karakter)">
                            <td>{{ karakter.nev }}</td>
                            <td>{{ karakter.hovatartozas }}</td>
                            <td>{{ karakter.becenev }}</td>
                        </tr>
                    </tbody>
                </table>
            </div>

            <!-- Kép megjelenítése, ha van kiválasztott karakter -->
            <div class="col-12 col-md-5" v-if="selectedKarakter">
                <img :src="`/public/${selectedKarakter.nev.toLowerCase()}.png`" alt="Kép" class="selected-image">
                <h2>{{ selectedKarakter.nev }}</h2>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    inject: ['keresoSzo'],
    data() {
        return {
            karakterek: [
                { id: 1, nev: "Alucard", hovatartozas: "Hellsing Organization", becenev: "Dracula" },
                { id: 2, nev: "Anderson", hovatartozas: "Iscariot", becenev: "Paladin" },
                { id: 3, nev: "Captain", hovatartozas: "Millennium", becenev: "The Wolfman" },
                { id: 4, nev: "Dornez", hovatartozas: "Hellsing Organization", becenev: "Angel of Death" },
                { id: 5, nev: "Major", hovatartozas: "Millennium", becenev: "Sturmbannführer" },
                { id: 7, nev: "Schrodinger", hovatartozas: "Millennium", becenev: "The Catboy" },
                { id: 8, nev: "Victoria", hovatartozas: "Hellsing Organization", becenev: "Draculina" },
                { id: 9, nev: "Wingates", hovatartozas: "Hellsing Organization", becenev: "Sir Integra" }
            ],
            selectedKarakter: null,
        };
    },
    methods: {
        selectKarakter(karakter) {
            this.selectedKarakter = karakter; // Kiválasztott karakter beállítása
        }
    },
    computed: {
        filteredKarakterek() {
            const keresendo = this.keresoSzo ? this.keresoSzo.toLowerCase() : '';
            return this.karakterek.filter(karakter => {
                return (
                    karakter.nev.toLowerCase().includes(keresendo) ||
                    karakter.hovatartozas.toLowerCase().includes(keresendo) ||
                    karakter.becenev.toLowerCase().includes(keresendo)
                );
            });
        }
    }
};
</script>

<style scope>
@font-face {
    font-family: 'Hellsing'; /* Példa betűtípus neve */
    src: url('/Van Helsing.ttf') format('truetype'); /* Fájl elérési út */
    font-weight: normal;
    font-style: normal;
}

h2 {
    text-align: center;  
    color: black;
    font-family: 'Hellsing', serif;
    font-size: 100px;
}
/* Kép stílus nagy méretben */
.selected-image {
  max-width: 100%;
  height: auto;
  border: 2px solid #8b0000;
  margin-top: 20px;
  width: 100%; /* A kép nagy legyen */
  height: auto;
}

/* Flexbox a táblázat és a kép középre igazításához */
.row {
    display: flex;
    justify-content: space-between;
    /* Középre igazítás */
}

/* Táblázat általános stílusa */
.table {
    margin-top: 20px;
    border: 2px solid #8b0000;
    /* Vörös szegély */
    background-color: #1a1a1a;
    /* Mélyfekete háttér */
    text-align: center
}

/* Fejlécek stílusa */
.table thead {
    background-color: #3b3b3b;
    /* Sötétszürke háttér a fejlécekhez */
    color: #ff0000;
    /* Vérvörös betűszín */
    font-family: 'Cinzel', serif;
    letter-spacing: 1px;
    text-transform: uppercase;
}

/* Táblázat sorainak stílusa */
.table tbody tr {
    background-color: #2c2c2c;
    /* Sötét sorok */
    color: #f5f5f5;
    /* Halvány fehér betűszín */
    font-family: 'Lora', serif;
    cursor: url('/cursor.png'), auto;
    transition: background-color 0.3s ease;
}

/* Hover hatás a táblázat soraiban */
.table tbody tr:hover {
    background-color: #3b3b3b;
    /* Világosabb sötétszürke, ha fölé viszed az egeret */
}

/* Cellák közti szegély */
.table td,
.table th {
    border-color: #8b0000;
    /* Vörös szegélyek a cellák között */
    padding: 15px;
    /* Extra padding a cellákban */
}

/* Általános stílus az oldalhoz */
body {
    background-color: #0d0d0d;
    /* Mély fekete háttér */
    color: #f5f5f5;
    /* Halvány fehér szöveg */
    font-family: 'Lora', serif;
    /* Kifinomult serif betűtípus */
}

/* Hover effekt a táblázat linkjein */
.table tbody tr:hover td {
    color: #ff0000;
    /* Vörös színűvé válnak a szövegek hover esetén */
}

/* Táblázat fejléc betűtípusa és mérete */
.table thead th {
    font-size: 1.2rem;
    /* Fejléc betűméret növelése */
}

/* A sorok celláinak stílusa */
.table tbody td {
    font-size: 1rem;
    /* Szöveg mérete a sorokban */
}

/* Táblázatnál a fejléc sötétebb színe */
.table thead {
    background-color: #1a1a1a;
}

.table th {
    color: red;
}
</style>
