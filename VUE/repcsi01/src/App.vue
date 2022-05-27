<template>
  <form method="post" @submit.prevent="feltetel">
    <label for="szelsebesség">Szélsebesség</label>
    <input type="number" min="0" max="500" id="szelSebesség" v-model="szelSebesseg" required />

    <label for="szelirány">Szélirány</label>
    <input type="number" min="0" max="180" id="szelIrany" v-model="szelIrany" required />

    <label for="felhosodes">Felhősödés</label>
    <input type="number" min="0" max="100" id="felhosodes" v-model="felhosodes" required />

    <button type="submit">Repülhet-e?</button>
  </form>

  <p v-show="isCanFly"><strong>Repülhet1? </strong>{{ isCanFly }}</p>
  <p v-show="nemAjanlott"><strong>Repülhet2? </strong>{{ nemAjanlott }}</p>
  <p v-show="tiltottFelszallas"><strong>Repülhet3? </strong>{{ tiltottFelszallas }}</p>

 <ul> <li>1.        Kérjük be a szélsebességet (km/óra).</li>
<li>2.        Kérjük be az 1-s jelű kifutóhoz képest milyen szögben fúj a szél (szélirány).</li>
<li>3.        Kérjük be felhősödés arányszámát.</li>

<li>Ha a szélsebessége nagyobb mint 50 km/óra és 1-s kifutóhoz képest az eltérés nagyobb mint 30%, akkor írjuk ki, hogy "Nem ajánlott a felszállás".</li>

<li>Ha szél sebessége nagyobb mint 100 km/óra, a széliránytól függetlenül írjuk ki, hogy "Tiltott felszállás".</li>

<li>Ha a felhősödési arányszám nagyobb mint 45, akkor írassuk ki, hogy "Tiltott felszállás".</li>

<li>Ha a felhősödési arányszám nagyobb mint 45, akkor írassuk ki, hogy "Tiltott felszállás".</li>

<li>Ellenőrizzük a bemenő adatokat</li>
<li>1.        A szél sebessége nem lehet negatív érték és nagyobb mint 500 km/óra</li>
<li>2.        A szélirány 0 és 180 fok közötti érték lehet</li>
<li>3.        A felhősödési arányszám 1 és 100 közötti szám lehet. Ha felhasználó nem ebbe az intervallumba eső számot ír, figyelmeztessük.</li>
</ul>



</template>
<script>
export default {
  name: "App",
  data() {
    return {
      szelSebesseg: "",
      szelIrany: "",
      felhosodes: "",

      nemAjanlott: "",
      tiltottFelszallas: "",
      isCanFly: "",
    };
  },
  methods: {
    feltetel() {
      if (this.urlapellenorzes()) return;
      this.isCanFly="Szabad a felszállás" ;
    },
    urlapellenorzes() {
      let hiba = false;
      this.nemAjanlott = false;
      this.tiltottFelszallas = false;
      if (
        (this.szelSebesseg > 50 &
        this.szelIrany > 30 || this.szelIrany < 150))
         { this.nemAjanlott = true; hiba = true; return this.nemAjanlott="Nem ajánlott"; }
      if (
        (this.szelSebesseg > 100 || this.felhosodes > 45))
          {this.tiltottFelszallas = true; hiba = true; return this.tiltottFelszallas="Tiltott felszállás";}
      return hiba;
    },
  },
};
</script>

<style></style>
