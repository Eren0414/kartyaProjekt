<template>
    <div class="container-fluid">
        <div class="row justify-content-center"> <!-- Flexbox használata a középre igazításhoz -->
            <!-- Táblázatos megjelenítés a karakterekről -->
            <div class="col-md-8">
                <table class="table table-dark table-hover">
                    <thead>
                        <tr>
                            <th scope="col">Név</th>
                            <th scope="col">Hovatartozás</th>
                            <th scope="col">Becenév</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="character in filteredCharacters" :key="character.id">
                            <td>{{ character.cim }}</td>
                            <td>{{ character.affiliation }}</td>
                            <td>{{ character.alias }}</td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    inject: ['keresoSzo'], // A kereső szó hozzáférhetővé tétele
    data() {
        return {
            characters: [
                { id: 1, cim: "Alucard", affiliation: "Hellsing Organization", alias: "Dracula" },
                { id: 2, cim: "Anderson", affiliation: "Iscariot", alias: "Paladin" },
                { id: 3, cim: "Captain", affiliation: "Millennium", alias: "The Wolfman" },
                { id: 4, cim: "Dornez", affiliation: "Hellsing Organization", alias: "Angel of Death" },
                { id: 5, cim: "Major", affiliation: "Millennium", alias: "Sturmbannführer" },
                { id: 7, cim: "Schrodinger", affiliation: "Millennium", alias: "The Catboy" },
                { id: 8, cim: "Victoria", affiliation: "Hellsing Organization", alias: "Draculina" },
                { id: 9, cim: "Wingates", affiliation: "Hellsing Organization", alias: "Sir Integra" }
            ]
        };
    },
    computed: {
        filteredCharacters() {
            const keresendo = this.keresoSzo ? this.keresoSzo.toLowerCase() : '';
            return this.characters.filter(character => {
                return (
                    character.cim.toLowerCase().includes(keresendo) ||
                    character.affiliation.toLowerCase().includes(keresendo) ||
                    character.alias.toLowerCase().includes(keresendo)
                );
            });
        }
    }
};
</script>

<style scoped>
/* Sötét háttér és kontrasztos színek */
.container-fluid {
    margin-top: 20px;
    padding: 20px;
}

/* Flexbox a táblázat középre igazításához */
.row {
    display: flex;
    justify-content: center;
    /* Középre igazítás */
}

/* Táblázat általános stílusa */
.table {
    margin-top: 20px;
    border: 2px solid #8b0000;
    /* Vörös szegély */
    background-color: #1a1a1a;
    /* Mélyfekete háttér */
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
    cursor: url('public/cursor.png'), auto;
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
</style>
