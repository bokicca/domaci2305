# domaci2305
package com.bootcamp;
/*
Kreirati klasu Planina koju opisuju ime planine, naziv države u kojoj se nalazi i visina planine.
Klasa mora imati konstruktore i getere i setere.
*/

public class Planina {
    private String imePlanine;
    private String nazivDrzave;
    private int visinaPlanine;

    public Planina() {
    }

    public Planina(String imePlanine, String nazivDrzave, int visinaPlanine) {
        this.imePlanine = imePlanine;
        this.nazivDrzave = nazivDrzave;
        this.visinaPlanine = visinaPlanine;
    }

    public String getImePlanine() {
        return imePlanine;
    }

    public void setImePlanine(String imePlanine) {
        this.imePlanine = imePlanine;
    }

    public String getNazivDrzave() {
        return nazivDrzave;
    }

    public void setNazivDrzave(String nazivDrzave) {
        this.nazivDrzave = nazivDrzave;
    }

    public int getVisinaPlanine() {
        return visinaPlanine;
    }


    public void setVisinaPlanine(int visinaPlanine) {
        if (visinaPlanine < 0) {
            this.visinaPlanine = visinaPlanine;
        } else {
            System.out.println("Nevalidan unos.");
        }
}}



package com.bootcamp;
/*
* Kreirati klasu Planinar kog opisuju jedinstveni celobrojni identifikacioni broj, ime i prezime.
Svi podaci smeju da se dohvate, ali ne i postave mimo konstruktora koji postavlja sve attribute klase.
Pored toga, klasa ima:
- apstraktnu metodu štampaj
- apstraktnu metodu koja vraca clanarinu planinara
- apstraktnu metodu uspesanUspon koja vraća informaciju da li će se planinar upešno popeti na planinu.
Metoda kao ulazni parametar prima objekat tipa Planina.

     Sve vrednosti smeju da se dohvate, ali ne i postave znaci da ne smemo da imamo set metode
     */


public abstract class Planinar {
    private int idPlaninara;
    private String imePlaninara;
    private String prezimePlaninara;

    public Planinar() {
    }

    public Planinar(int idPlaninara, String imePlaninara, String prezimePlaninara) {
        this.idPlaninara = idPlaninara;
        this.imePlaninara = imePlaninara;
        this.prezimePlaninara = prezimePlaninara;
    }

    public int getIdPlaninara() {
        return idPlaninara;
    }


    public String getImePlaninara() {
        return imePlaninara;
    }


    public String getPrezimePlaninara() {
        return prezimePlaninara;
    }

    public abstract void stampaj ();
    public abstract int clanarinaPlaninara();
    public abstract boolean uspesanUspon(Planina planina);

    }

package com.bootcamp;
/*
Kreirati klasu RekreativniPlaninar koja pored svega što ima Planinar ima i:
    - težinu opreme (kg) koju nosi (celobrojna je vrednost npr: 20kg),
    - naziv okruga odakle je rekreativni planinar
    - maksimalni uspon koji planinar može da savlada bez opreme (npr: 2000m)
    - da li će rekreativni planinar uspešno popeti na planinu zavisi da li je njegov najveći uspon manji od visine planine,
      s tim da oprema dodatno otežava penjanje i za svaki kilogram opreme koji nosi može da pređe 50 metara manje.
    - rekeativci placaju clanarinu u iznosu od 1000 rsd
    - metoda koja ispisuje podatke o planinaru ispisuje ih u sledećem formatu:
        Rekreativac, id: id
        ime: ime prezime Okrug: okrug
*/

public class RekreativniPlaninar extends Planinar {
    private int tezinaOpreme;
    private String nazivOkruga;
    private double maksimUsponBezOpreme;



    public RekreativniPlaninar(int idPlaninara, String imePlaninara, String prezimePlaninara, int tezinaOpreme,
                               String nazivOkruga, double maksimUsponBezOpreme){
        super ( idPlaninara, imePlaninara, prezimePlaninara);
        this.tezinaOpreme = tezinaOpreme;
        this.nazivOkruga = nazivOkruga;
        this.maksimUsponBezOpreme = maksimUsponBezOpreme;
    }

    public int getTezinaOpreme() {
        return tezinaOpreme;
    }

    public String getNazivOkruga() {
        return nazivOkruga;
    }

    public double getmaksimUsponBezOpreme() {
        return maksimUsponBezOpreme;
    }


    public void stampaj (){
        System.out.println("Rekreativac, id: " +  getIdPlaninara() +
                " ime:" + getImePlaninara() +  getPrezimePlaninara() +  " Okrug: " + getNazivOkruga()
        );
    }



    public int clanarinaPlaninara (){
        return 1000;
    }
    public boolean uspesanUspon( Planina planina) {
        if((maksimUsponBezOpreme - getTezinaOpreme()*50) < planina.getVisinaPlanine()){
            return true;
        }else {
            return false;
        }
    }



}


package com.bootcamp;
/*
Kreirati klasu Alpinista koji dodatno pamti koliko poena je alpinista ostvario (celobrojna vrednost) i
poeni se mogu menjati kroz adekvatnu metodu. Alpinista može da savlada sve uspone do 4000 metara,
placa clanarinu u iznosu od 1500 pritom za svaki poen ima popust od 50, a informacije o alpinisti se ispisuju u formatu:
    Alpinista, id: id
    ime: ime i prezime
    Broj poena: poeni
*/

public class Alpinista extends Planinar {
    private int poen;

    public Alpinista ( int idPlaninara, String imePlaninara, String prezimePlaninara, int poen){
        super (idPlaninara, imePlaninara, prezimePlaninara);
        this.poen= poen;
    }

    public int getPoen() {
        return poen;
    }
    public void stampaj (){
        System.out.println("Alpinista, id: " +  getIdPlaninara() +
                " ime: " + getImePlaninara() +  getPrezimePlaninara() +  " Broj poena: " + getPoen()
        );
    }
    public int clanarinaPlaninara () {
        int novaClanarina = 1500 - this.poen * 50;
        if(novaClanarina > 0){
            return novaClanarina;
        }else{
            return 0;
        }
    }




    public boolean uspesanUspon (Planina planina){
        if (planina.getVisinaPlanine()< 4000){
            return true;
        }else{
            return false;
        }
    }
}


package com.bootcamp;

import java.util.ArrayList;
/*
Kreirati glavnu klasu I u njoj:
    - instancirati jednu planinu
    - napraviti niz ili listu koji ce sadrzati najmanje tri rekrativna planinara I tri alpiniste
    - ispisati podatke o svim planinarima I za svakog od planinara ispisati da li ce se popeti na instanciranu planin
    - ispisati kolika je zbir svih clanarina planinara iz niza/liste
*/

public class Main {
    public static void main(String[] args) {
        Planina planina = new Planina("Jahorina", "BiH", 1916);

        ArrayList<Planinar>listaPlaninara = new ArrayList<>();

        listaPlaninara.add(new Alpinista(1,"Bojana ", "Bozovic", 333));
        listaPlaninara.add(new Alpinista(2, "Marko" , "Markovic", 444));
        listaPlaninara.add(new Alpinista(3, "Darko ", "Jerkovic", 555));
        listaPlaninara.add(new RekreativniPlaninar(4, "Slavko ", "Slavkovic", 15, "Backa", 1915));
        listaPlaninara.add(new RekreativniPlaninar(5, "Djordje ", "Djordjevic", 16, "Vojvodina", 2116));
        listaPlaninara.add(new RekreativniPlaninar(6, "Petar ", "Petrovic", 20, "Vojvodina", 8848));

        for (Planinar pl: listaPlaninara){
            pl.stampaj();

        }
        for (Planinar pl: listaPlaninara){
            System.out.println("Planinar " + pl.getImePlaninara()+ " " + pl.getPrezimePlaninara() + " se uspjesno popeo na vrh "
                    + planina.getImePlanine() + " = " + pl.uspesanUspon(planina));

        }
        double suma = 0;
        for (Planinar pl : listaPlaninara){
            suma += pl.clanarinaPlaninara();
        }
        System.out.println("Zbir svih clanarina je: " + suma);
    }

}
