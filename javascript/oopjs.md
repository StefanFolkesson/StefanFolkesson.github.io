# OOP i Javascript
## Vad är en klass?
Definitionen av en sak.
```javascript
class Name {

}
```
En klass bör ha en konstruktor:
```javascript
class Name {
    constructor(indata){
        this.indata = indata;
    }
}
```
Konstruktorn körs varje gång du skpar en instans av klassen. ( Initierar insansen) Mer om det vid nästa fråga "Vad är en instans". 
En klass kan ha attribut och funktioner. I exemplet ovan skapar jag ett attribut som heter indata. Med this hänvisar jag till klassen.
this.indata betyder indata är ett attribut i klassen.
En funktion deklarerar jag precis på samma sätt som jag brukar med den enda skillnaden att funktionen skall vara i klassen.
```javascript
class Name {
    visaNamn(){
        console.log(this.namn)
    }
}
```
# Vad är en instans?
En sak av typen klass.
En instans är en skapelse av klassen. Om klassen heter Stol så kan instansen vara just den stolen jag sitter på. låt mig visa ett exempel:

Jag skapar en klass som heter karaktär och en instans av klassen som heter spelare:
```javascript
class Karaktär{
    constructor(name,level,hp,inventory){
        this.name=name;
        this.level=level;
        this.hp=hp;
        this.inventory = [...inventory];
    }
    changeLevel(inc){
        if(inc<0)
            if(this.level>1){
                this.level+=inc;
                this.hp+=inc*8;
            }
            else
                return; // Kan inte levla under 1
        else{
            this.level+=inc;
            this.hp+=inc*8;
        }
    }
    changeHp(value){
        this.hp+=value;
    }
    getStatus(){
        if(this.hp>0)
            return "Alive";
        else
            return "Dead";
    }
}
spelare = new Karaktär("Gandalf",1,1,["Staff","Robe"]);
spelare.changeLevel(1);
console.log(spelare.getStatus())
spelare.changeHp(-30);
console.log(spelare.getStatus())
```

## Arv (Inheritance)
När en klass kan ärva egenskaper från en annan klass.
Förklaras nog bäst med exempel.
Jag har en klass som jag kallas spelobjekt den håller reda på sin position. Det kommer vara en abstrakt klass dvs den kommer inte användas som avbild till en instans (Ingenting kan vara bara ett spelobjekt). Men jag använder den sombas till alla saker i mit spel en dörr som skall öppnas är ett spelobject och spelaren är ett spel object. båda två har en grafisk representation och en position i spelet. Så spelobject har position och bild som attribut och varför inte rita ut sig som funktion.
```javascript
class Position {
    constructor(x,y){
        this._x=x;
        this._y=y;
    }
    get x(){
        return this._x;
    }
    get y(){
        return this._y;
    }

    set x(value){
        this._x=value;
    }
    set y(value){
        this._y=value;
    }
}


class Spelobjekt {
    constructor(pos,image){
        // Jag vill ha pos som en egen klass med ett x och ett y värde
        this.pos=pos;
        this.image=image;
    }
    rita(context){
        console.log(this.pos.x,this.pos.y);
        context.drawImage(this.image,this.pos.x,this.pos.y);
    }
}

class Dörr extends Spelobjekt{
    constructor(pos,image,image2){
        super(pos,image);
        this.image2=image2;
        this.status="stängd";
    }
    öppnaDörr(){
        if(this.status=="stängd"){
            this.status="öppen";
        } else {
            console.log("Dörren är redan öppen");
            return;
        }
    }
}

class Spelare extends Spelobjekt{
    constructor(pos,image){
        super(pos,image);
        this.hårfärg = "brun";
    }
}

let dörr1 = new Dörr(new Position(10,10),"dörr.png","öppendörr.png");
let spelare1 = new Spelare(new Position(10,10),"kalle.png");

dörr1.rita();
spelare1.rita();
dörr1.visaStatus();
```
Båda instanserna använder sig av Rita funktionen i klassen men de använder sina egna attribut.



## Polymorfism
Du kan ha flera metoder med samma namn men olika parametrar och de gör olika saker. 
Ett sätt att hantera polymorfism är att göra överlagringar på metoder i arvet.
Faktum är att vi redan gjort det med konstruktorn. Dörr och Spelare har sina egna konstruktorer och kallar på Spelobjektskonstruktorn med hjälp av det inbyggda reserverade ordet super.
```javascript
class Spelare extends Spelobjekt{
    constructor(pos,image){
        super(pos,image);
        this.hårfärg = "brun";
    }
}
```
Samma sak har vi när vi skall hantera rita funktionen i Dörr klassen. Om dörren har status öppen skall vi visa en bild annars skall vi visa enannan. 
```javascript
    rita(context){
        if(this.status="öppen")
            context.drawImage(this.image2,this.pos.x,this.pos.y);
        else
            super.rita();
    }
```
## Abstraktion
Visar det som är relevant för användaren ( Public, Private) ( Ej i Javascript)
## Encapsulation
När man för attributen idiotsäker med set och get.
Ett exempel på encapsulation är Punkt. Där säkerställer vi att x och y innehåller rätt värden genom att köra över hur vi hanterar = (tilldelning). Vid varje tilldelning så tvingar vi klassen att köra set funktionen. 
Ex:
```javascript
class Position {
    constructor(x,y){
        this._x=x;
        this._y=y;
    }
    get x(){
        return this._x;
    }
    get y(){
        return this._y;
    }

    set x(value){
        if(value<0)
            return;
        this._x=value;
    }
    set y(value){
        if(value<0)
            return;
        this._y=value;
    }
}
p = new Position(20,20);
p.x = 40;  // Kör set x(value)
p.x=-2; // Nekas eftersom value är mindre än 0, Ingen ändring sker.
```

