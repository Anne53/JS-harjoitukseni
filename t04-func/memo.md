//Mainio matsku löytyy: https://github.com/tahuomo/javascript-s2013/wiki/Viikko-3-oliot-ja-periytyminen (Vilpponen löysi)

//Esimerkki "luokan" luomisesta: konstruktori? attribuutit ja "metodi"

function Ihminen(nimi, syntymavuosi) {
    this.nimi = nimi;
    this.syntymavuosi = syntymavuosi;
    this.esittaydy = function(){alert(this.nimi + ", syntynyt " + this.syntymavuosi)}
}

/*
Olioiden kentät ovat suojaamattomia ja avoimia. Olioille ja luokille on dynaamisesti mahdollista lisätä, poistaa tuo muokata kenttiä. Mikäli luokalta puuttuu jokin oleellinen funktio tai kenttä, sellaisen voi asettaa sille.
Vaikkakin arvojen lisääminen ja korvaaminen voi olla vaarallista, se mahdollistaa myös uusi tapoja uudelleenkäyttää koodia. On esimerkiksi mahdollista tehdä funktio, joka lisää sille parametrina annetulle oliolle uuden funktion.
*/

opetaUimaan = function(ihminen){

     ihminen.ui = function(){return "puli puli molskis"}
}

var soini = new Ihminen("Timo Soini", 1962)
soini.ui // undefined
soini.ui() // TypeError: Object #<Ihminen> has no method 'ui'

opetaUimaan(soini)
soini.ui // function(){return "puli puli molskis"}
soini.ui() // "puli puli molskis"

/*
Jos yksittäisen olion sijaan halutaankin lisätä uusi arvo kokonaiselle luokalle, on sekin täysin mahdollista lennosta. Tällöin uudet ominaisuudet määritellään luokan prototyypille.
*/

Ihminen.prototype.jalkojenMaara = 2
Ihminen.prototype.puhu = function(){return "Nyt tuli jytky!"}

soini.jalkojenMaara // 2
soini.puhu() // "Nyt tuli jytky!"

//Vaikka JavaScript ei sinänsä tuekaan moniperintää, voidaan oloihin “sekoittaa” toisen olion ominaisuuksia (mixin):

var KissaMixin = function() {
    this.mourua = function() { alert("miau"); };
}
KissaMixin.call(Poliitikko.prototype);
soini.mourua(); // Ilmoitus: "miau"

//Tässä siis poliitikon prototyyppiin sekoitettiin kissamainen ominaisuus.

