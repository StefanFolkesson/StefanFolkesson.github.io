# Creating a Simple Game

För att skapa ett enkelt spel måste vi först ha några karaktärer.
Varför inte börja med Den episka striden i Morias grottor mellan Gandalf och Balrogen. 

Vi måste lagra våra karaktärers namn.

```python
spelare = "Gandalf"
fiende = "Balrog"
```
Till vänster om likamedtecknet har vi något vi kallar en variabel. Denna variabel innehåller det som är till höger om likamedtecknet.
Så vi har skapar två variabler: spelare och fiende  som innehåller namnet på våra karaktärer. Enkelt. 
Låt oss presentera fighten för vår användare genom att skriva ut på skärmen med hjälp av kommandont print.
```python
print("Den mäktiga striden i Morias grottor är påväg att starta")
```
För att hämta innehållet i variablerna skriver man bara variablernas namn:
```python
print(spelaren + "står på bron och tittar ned på " + fienden + " i avgrunden")
```

Vi kan även hålla reda på livet på våra karaktäerer. 
```python
spelare_liv = 100
fiende_liv = 100
```
Vad jag kallar variablerna är inte viktigt. Så länge de är lokiska för mig. I Detta fall känndes det bra att "koppla" livet till karaktären.

Nu till vapen. Vad har Gandalf att slåss med. En stav. Hrmm... Inte så mäktigt men effektivt. 
```python
spelare_vapen="Stav"
spelare_vapen_skada=10
```
Och Balrogen då. Han har en piska om jag inte missminner mig. 
```python
fiende_vapen="Piska"
fiende_vapen_skada=30
```
Så hur ser vår kod ut nu:
```python
spelare = "Gandalf"
spelare_liv = 100
spelare_vapen="Stav"
spelare_vapen_skada=10

fiende = "Balrog"
fiende_liv = 100
fiende_vapen="Piska"
fiende_vapen_skada=30

print("Den mäktiga striden i Morias grottor är påväg att starta.")
print(spelaren + "står på bron och tittar ned på " + fienden + " i avgrunden")

```

Nu kan vi börja slåss:

```python
print(spelare + " slår med sin " +spelare_vapen +" och gör: "+ str(spelare_vapen_skada) +" skada")
fiende_liv = fiende_liv - spelare_vapen_skada
print(fiende + " har nu bara " + str(fiende_liv)+ " hälsopoäng kvar")
```
Här hände det mycket + betyder att vi slåt ihop texterna. sen har vi str(spelare_vapen_skada) till exempel. spelare_vapen_skada innehåller ett tal (10 om jag inte missminner mig). Detta är ett problem så vi behöver göra om talet till en text och text i python heter string så str() är en förkortning till "gör om det i parentesen till en text" .

Hela programmet:

```python
spelare = "Gandalf"
spelare_liv = 100
spelare_vapen="Stav"
spelare_vapen_skada=10

fiende = "Balrog"
fiende_liv = 100
fiende_vapen="Piska"
fiende_vapen_skada=30

print("Den mäktiga striden i Morias grottor är påväg att starta.")
print(spelaren + "står på bron och tittar ned på " + fienden + " i avgrunden")

print(spelare + " slår med sin " +spelare_vapen +" och gör: "+ str(spelare_vapen_skada) +" skada")
fiende_liv = fiende_liv - spelare_vapen_skada
print(fiende + " har nu bara " + str(fiende_liv)+ " hälsopoäng kvar")
```
## Lägga till val
Allt detta är statiskt. För varje gång som vi kör programmet kommer det alltid se ut som det gör. 
Om vi skall göra detta till ett spel och inte bara en saga (där allting sker på samma sätt varje gång) så kanske vi vill lägga till lite interaktivitet.
Interaktivitet får man genom att låta användaren påverka saker. 
Jag vill kanske döpa om min spelarkaraktär. 
```python
spelare = input("Vad vill du att din spelare skall heta?")
```
Med hjälp av input() kan jag som spelare mata in saker till datorn med tangentbordet. Det som jag skriver innom parentesen är den text som kommer upp på skärmen innan jag matar in. 
Precis som förut så sparar vi namnet i variabeln spelare. Så vi lätt kan ta fram det när vi vill använda det i vår berättelse. 
```python
print("Var hälsad, "+spelare+"!")
```
Ett annat sätt att skapa interaktivitet är att låta spelaren bestämma saker i till exempel en strid. 
```python
svar = input("Vad vill du göra härnäst? (slå/fly) ")
if(svar=="slå"):
    print(spelare + " slår med sin " +spelare_vapen +" och gör: "+ str(spelare_vapen_skada) +" skada")
    fiende_liv = fiende_liv - spelare_vapen_skada
    print(fiende + " har nu bara " + str(fiende_liv)+ " hälsopoäng kvar")
else:
    print("Du flyr!")
```
## Upprepning
Vi skulle vilja fortsätta slå tills någon har vunnit/förlorat. För att hantera detta använder vi så kallade loopar.
Det finns två sätt att hantera loopar antingen så loopar man ett bestämt antal gånger eller så loopar man tills ett
villkor uppfylls. I detta fall vet vi inte hur många gångar vi behöver slå tills vi vunnit. Så vi sätter ett villkor så länge mitt liv är över 0 och fiendens liv är över 0.
```python
while(spelare_liv > 0 and fiende_liv > 0):
    # Slåss!!
```
Så då kan vi lägga in slagsmålet i loopen. Jag slår, han slår och så fortsätter vi tills någon har 0 liv.
```python
while(spelare_liv > 0 and fiende_liv > 0):
    # Du slår
    print(spelare + " slår med sin " +spelare_vapen +" och gör: "+ str(spelare_vapen_skada) +" skada")
    fiende_liv = fiende_liv - spelare_vapen_skada
    print(fiende + " har nu bara " + str(fiende_liv)+ " hälsopoäng kvar")
    # Fiende slår
    print(fiende + " slår med sin " +fiende_vapen +" och gör: "+ str(fiende_vapen_skada) +" skada")
    spelare_liv = spelare_liv - fiende_vapen_skada
    print(spelare + " har nu bara " + str(spelare_liv)+ " hälsopoäng kvar")

```

Nu skulle vi kunna lägga till valet in i upprepningen. Om jag väljer att fly så får fienden slå på mig en gång men 
sen är striden slut. Då måste vi antingen lägga till ett extra villkor i loopen eller så gör vi ett avbrott (break).
Jag väljer att göra ett break för jag tycker det passar bäst in för oss. 
```python
while(spelare_liv > 0 and fiende_liv > 0):
    svar = input("Vad vill du göra härnäst? (slå/fly) ")
    if(svar=="slå"):
        # Du slår
        print(spelare + " slår med sin " +spelare_vapen +" och gör: "+ str(spelare_vapen_skada) +" skada")
        fiende_liv = fiende_liv - spelare_vapen_skada
        print(fiende + " har nu bara " + str(fiende_liv)+ " hälsopoäng kvar")
    # Fiende slår
    print(fiende + " slår med sin " +fiende_vapen +" och gör: "+ str(fiende_vapen_skada) +" skada")
    spelare_liv = spelare_liv - fiende_vapen_skada
    print(spelare + " har nu bara " + str(spelare_liv)+ " hälsopoäng kvar")
    if(svar=="fly"):
        print("Du flyr!")
        break    
```
## Sammanställning
Nu har du grunderna till att göra ett enkelt äventyrsspel. 
```python
spelare = "Gandalf"
spelare_liv = 100
spelare_vapen="Stav"
spelare_vapen_skada=10

fiende = "Balrog"
fiende_liv = 100
fiende_vapen="Piska"
fiende_vapen_skada=30

print("Den mäktiga striden i Morias grottor är påväg att starta.")
print(spelaren + "står på bron och tittar ned på " + fienden + " i avgrunden")

while(spelare_liv > 0 and fiende_liv > 0):
    svar = input("Vad vill du göra härnäst? (slå/fly) ")
    if(svar=="slå"):
        # Du slår
        print(spelare + " slår med sin " +spelare_vapen +" och gör: "+ str(spelare_vapen_skada) +" skada")
        fiende_liv = fiende_liv - spelare_vapen_skada
        print(fiende + " har nu bara " + str(fiende_liv)+ " hälsopoäng kvar")
    # Fiende slår
    print(fiende + " slår med sin " +fiende_vapen +" och gör: "+ str(fiende_vapen_skada) +" skada")
    spelare_liv = spelare_liv - fiende_vapen_skada
    print(spelare + " har nu bara " + str(spelare_liv)+ " hälsopoäng kvar")
    if(svar=="fly"):
        print("Du flyr!")
        break    
```
## Slump
Just nu är det ganska uppenbart att Balrogen vinner. Det är lite tråkigt. Vi kan lägga till lite slump. Det är helt
enkelt så att vi kan få datorn att ta fram ett tal mellan två olika värden. 
Detta innebär att vi behöver göra om lite hur vi hanterar vapnen. Vi får sätta ett minimun värde och ett maximum 
värde.
```python
spelare_vapen_skada_min=10
spelare_vapen_skada_max=20
fiende_vapen_skada_min=1
fiende_vapen_skada_max=30
# För att få fram skadan använder man sig av ett bibliotek som heter random.
import random
# Denna skall vara högst upp i dokumentet.

# Sedan i loopen kan vi lägga till dessa rader direkt efter frågan vad vill du göra härnäst. :
spelare_vapen_skada = random.randint(spelare_vapen_skada_min,spelare_vapen_skada_max)
fiende_vapen_skada = random.randint(fiende_vapen_skada_min,fiende_vapen_skada_max)
```
Tillsist kanske vi skall ha en hantering om du dog eller om fienden dog. 
```python
if(spelare_liv<=0):    
    print("Du dog!")
if(fiende_liv<=0):    
    print("Fienden dog!")
```
Slutprodukten ser ut såhär

```python
import random

spelare = "Gandalf"
spelare_liv = 100
spelare_vapen="Stav"
spelare_vapen_skada=10
fiende = "Balrog"
fiende_liv = 100
fiende_vapen="Piska"
fiende_vapen_skada=30
spelare_vapen_skada_min=10
spelare_vapen_skada_max=20
fiende_vapen_skada_min=1
fiende_vapen_skada_max=30

print("Den mäktiga striden i Morias grottor är påväg att starta.")
print(spelare + "står på bron och tittar ned på " + fiende + " i avgrunden")

while ((spelare_liv > 0) and (fiende_liv > 0)) :
    svar = input("Vad vill du göra härnäst? (slå/fly) ")
    spelare_vapen_skada = random.randint(spelare_vapen_skada_min,spelare_vapen_skada_max)
    fiende_vapen_skada = random.randint(fiende_vapen_skada_min,fiende_vapen_skada_max)
    if(svar=="slå"):
        # Du slår
        print(spelare + " slår med sin " +spelare_vapen +" och gör: "+ str(spelare_vapen_skada) +" skada")
        fiende_liv = fiende_liv - spelare_vapen_skada
        print(fiende + " har nu bara " + str(fiende_liv)+ " hälsopoäng kvar")
    # Fiende slår
    print(fiende + " slår med sin " +fiende_vapen +" och gör: "+ str(fiende_vapen_skada) +" skada")
    spelare_liv = spelare_liv - fiende_vapen_skada
    print(spelare + " har nu bara " + str(spelare_liv)+ " hälsopoäng kvar")
    if(svar=="fly"):
        print("Du flyr!")
        break    
if(spelare_liv<=0):    
    print("Du dog!")
if(fiende_liv<=0):    
    print("Fienden dog!")
```
## Nytt rum
Nu skall vi kanske försöka styra upp hela spelet med att vi kan gå från olika platser 
När vi flytt från Balrogen, eller för den delen bekämpat honom. Så vill vi kanske gå vidare. 
Om vi flyr skall vi automatiskt gått till nästa plats. Men om vi bekämpar honom måste vi få valet att gå til nästa plats. 
Så låt oss skapa nästa rum efter vi flytt. 
```python
.
.
.
if(spelare_liv<=0):    
    print("Du dog!")
    exit()
if(fiende_liv<=0):    
    print("Fienden dog!")
## Rum 2
print("Utanför berget")
print(spelare +" lyckades ta sig ut.")
print(spelare + " ser en stig")
val = input("Vad gör du? (stanna) kvar/(springa) nedför stigen: ")
if(val=="stanna"):
    print("Berget verkar explodera under dig och du brinner upp.")
    exit()
else:
    print("När du springer ned för bergskanten ser du bakom dig hur hela berget börjar brinna")

```
Jag har lagt till en ny inbyggd funktion som helt enkelt avslutar programmet tvärt. Och det är exit(). Det gör att det är enklare att hantera rumsbyten. När du dör så stänger programmet ner helt enkelt. 

## Plocka upp saker

Natten faller på och du behöver leta efter en pinne och göra eld av.
Så vi skulle vilja ha en inventory att ta hand om. För enkelthets skull så kan vi bara ha en sak i inventory åt gången.

```python
## Rum 3
print(spelaren +" står vid foten till berget och bestämmer sig för att ta en paus")
print("Framför dig ligger en pinne")
val = input("Vad vill du göra? (Plocka upp pinne/Göra eld/Sova)")
```
Oj tre val. Med lite olika val i sig. 
Om jag gör upp eld utan att plocka upp pinnen så går det inte och jag kommer tillbaka.
Om jag Sover utan att ha gjort upp eld förfryser jag.
Om jag plockar upp pinnen skall den försvinna från prompten.
Om jag gör upp elt efter att jag plockat upp pinnen skall jag få en eld och prompten skall bara vara sova.
Om jag sover efter jag plockat upp pinnen utan att göra eld förfryser jag. 
så låt oss skapa tre variabler.
och vi gör om val=... raden
```python
pinne=True
eld=False
sova=False
while(sova==False):
    prompt="("
    if(pinne==True):
        prompt=prompt+"Plocka upp pinne /"
    if(eld==True):
        prompt=prompt+"en brinnande eld/Sova):"
    else:
        prompt=prompt+"göra en eld/Sova):"
    val=input(prompt)
    if(val == "plocka"):
        if(pinne==False): ## Jag har plockat upp pinnen
            print("Du har redan plockat upp pinnen")
        else:
            print("Du plockar upp pinnen")
            pinne=False
    elif(val == "elda"):
        if(eld==True):
            print("Din eld brinner redan.")
        else:
            if(pinne==False):
                print("Du tänder en eld!")
                eld=True
            else:
                print("Du behöver en pinne till det")
    elif(val=="sova"):
        if(eld==False):
            print("Du fryser ihjäl under natten")
            exit()
        if(eld==True):
            print("Du sover gott och vaknar nästa morgon")
            sova=True
    else:
        print("skriv plocka,elda eller sova")
```    
Sammanfattning
---
```python
import random

spelare = "Gandalf"
spelare_liv = 100
spelare_vapen="Stav"
spelare_vapen_skada=10
fiende = "Balrog"
fiende_liv = 100
fiende_vapen="Piska"
fiende_vapen_skada=30
spelare_vapen_skada_min=10
spelare_vapen_skada_max=20
fiende_vapen_skada_min=1
fiende_vapen_skada_max=30

print("Den mäktiga striden i Morias grottor är påväg att starta.")
print(spelare + "står på bron och tittar ned på " + fiende + " i avgrunden")

while ((spelare_liv > 0) and (fiende_liv > 0)) :
    svar = input("Vad vill du göra härnäst? (slå/fly) ")
    spelare_vapen_skada = random.randint(spelare_vapen_skada_min,spelare_vapen_skada_max)
    fiende_vapen_skada = random.randint(fiende_vapen_skada_min,fiende_vapen_skada_max)
    if(svar=="slå"):
        # Du slår
        print(spelare + " slår med sin " +spelare_vapen +" och gör: "+ str(spelare_vapen_skada) +" skada")
        fiende_liv = fiende_liv - spelare_vapen_skada
        print(fiende + " har nu bara " + str(fiende_liv)+ " hälsopoäng kvar")
    # Fiende slår
    print(fiende + " slår med sin " +fiende_vapen +" och gör: "+ str(fiende_vapen_skada) +" skada")
    spelare_liv = spelare_liv - fiende_vapen_skada
    print(spelare + " har nu bara " + str(spelare_liv)+ " hälsopoäng kvar")
    if(svar=="fly"):
        print("Du flyr!")
        break    
if(spelare_liv<=0):    
    print("Du dog!")
if(fiende_liv<=0):    
    print("Fienden dog!")
## Rum 2
print("Utanför berget")
print(spelare +" lyckades ta sig ut.")
print(spelare + " ser en stig")
val = input("Vad gör du? (stanna) kvar/(springa) nedför stigen: ")
if(val=="stanna"):
    print("Berget verkar explodera under dig och du brinner upp.")
    exit()
else:
    print("När du springer ned för bergskanten ser du bakom dig hur hela berget börjar brinna")
## Rum 3
print(spelaren +" står vid foten till berget och bestämmer sig för att ta en paus")
print("Framför dig ligger en pinne")
pinne=True
eld=False
sova=False
while(sova==False):
    prompt="("
    if(pinne==True):
        prompt=prompt+"Plocka upp pinne /"
    if(eld==True):
        prompt=prompt+"en brinnande eld/ Sova):"
    else:
        prompt=prompt+"göra en eld/ Sova):"
    val=input(prompt)
    if(val == "plocka"):
        if(pinne==False): ## Jag har plockat upp pinnen
            print("Du har redan plockat upp pinnen")
        else:
            print("Du plockar upp pinnen")
            pinne=False
    elif(val == "elda"):
        if(eld==True):
            print("Din eld brinner redan.")
        else:
            if(pinne==False):
                print("Du tänder en eld!")
                eld=True
            else:
                print("Du behöver en pinne till det")
    elif(val=="sova"):
        if(eld==False):
            print("Du fryser ihjäl under natten")
            exit()
        if(eld==True):
            print("Du sover gott och vaknar nästa morgon")
            sova=True
    else:
        print("skriv plocka,elda eller sova")
```
I ett val kan vi välja två olika saker. I detta fall höger eller vänster och varje val ger oss möjligheten att komma till ett nytt rum. 
För att hantera detta på ett enkelt sätt tar jag in några nya saker. 
Först och främst så låter har whileloopen hålla på tills val innehåller antingen höger eller vänster. 
Jag skapar en lista (en variabel som innehåller flera värden) som innehåller alla korrekta värden som du kan skriva in om du skriver något annat så kommer det som står i else: skrivas ut. 
val not in []  -> val inte finns i listan [] och val är det jag skrivit in. 
Sen skapar jag även en variabel rum. Jag sätter den på 3 för det är ju där vi är just nu. Om du skriver vänster så blir variabl rum 4 eller höger så blir den 5. Sen kollar jag efteråt vilken siffra rummet har så kan jag fortsätta där. Så i princip skulle jag kunna hantera rum i fortsättningen. När du gör något för att byta rum så sätter jag rumsvariabeln till det rum jag vill hoppa till (hellst hödre än det som är just nu annars blir det lite jobbigt) och sedan gör jag en break dvs avbryter den if-sats jag är i just nu för att till sist söka reda på nästa rum.

```python
rum = 3
while (val not in ["höger","vänster"]):
    val = input("Vägen delar sig i två delar (höger/vänster) vilken tar du?")
    if(val=="höger"):
        ## Rum 4
        rum = 4
    elif(val=="vänster"):
        ## Rum 5
        rum = 5
    else:
        print("Skriv 'höger' eller 'vänster'")
    

if(rum==4):
    print("Du kommer fram till en stuga")


if(rum==5):
    print("Du kommer fram till en sjö")
```

Old stuff
------
Detta skulle vi kunna göra genom att helt enkelt ha en lista med alla platser som vi kan vara på. Den första platsen är bron och nästa plats är utanför berget. 
sen sätter vi en stor loop runt om hela spelet (nästan)
```python
platser = ["På sista bron i moria","Utanför berget"]
plats = 0
while (plats<len(platser)):
    print(platser[plats])
    if(plats==0):
        if((spelare_liv > 0) and (fiende_liv > 0)):
            print("Den mäktiga striden i Morias grottor är påväg att starta.")
            print(spelare + "står på bron och tittar ned på " + fiende + " i avgrunden")

            while ((spelare_liv > 0) and (fiende_liv > 0)) :
                svar = input("Vad vill du göra härnäst? (slå/fly) ")
                spelare_vapen_skada = random.randint(spelare_vapen_skada_min,spelare_vapen_skada_max)
                fiende_vapen_skada = random.randint(fiende_vapen_skada_min,fiende_vapen_skada_max)
                if(svar=="slå"):
                    # Du slår
                    print(spelare + " slår med sin " +spelare_vapen +" och gör: "+ str(spelare_vapen_skada) +" skada")
                    fiende_liv = fiende_liv - spelare_vapen_skada
                    print(fiende + " har nu bara " + str(fiende_liv)+ " hälsopoäng kvar")
                # Fiende slår
                print(fiende + " slår med sin " +fiende_vapen +" och gör: "+ str(fiende_vapen_skada) +" skada")
                spelare_liv = spelare_liv - fiende_vapen_skada
                print(spelare + " har nu bara " + str(spelare_liv)+ " hälsopoäng kvar")
                if(svar=="fly"):
                    print("Du flyr!")
                    plats=plats+1

                    break    
            if(spelare_liv<=0):    
                print("Du dog!")
            if(fiende_liv<=0):    
                print("Fienden dog!")
        else:
            if(input("Du kan gå ut ur berget vill du det? (ja/nej)")=="ja"):
                plats=plats+1
    else:
        print("Du lyckades ta dig ut.")
        break
```
Lite nya saker här. 
Vu har en lista med platser och första platsen i den listan är position 0. Så är det helt enkelt i programmeringsvärlden. 
För att komma åt saker i listan använder man hakparenteser [] och där i skriver man platsens id så: platser[0] kommer ge oss svaret: "På sista bron i moria".
Vi använder även en inbyggd funktion len() som helt enkelt mäter längden på listan. 
Så len(platser) ger oss 2. 

Ditt uppdrag är att skapa ett enkelt spel där man kan bestämma sitt namn och där jag kan slåss mit en motståndare. 
Om jag överlever efter jag slagit så har jag vunnit. 