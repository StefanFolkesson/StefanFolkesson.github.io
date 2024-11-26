### Databas skola ###
Låt oss disskutera (eller jag kommer ranta på med min monolog) problematiken med att göra ett närvarosystem.
Vad är det man behöver för att hålla reda på en elev under en dag. 
Vi har Lektion, Klass, Ämne, Lärare, Elev, Klassrum, Längd

En elev har en klass i ett klassrum med ett ämne och  en lärare vid en tid. Detta kallas lektion vid den lektionen har eleven närvaro. Lektionen upprepas varje vecka och man kan vara närvarande på en lektion en vecka men frånvarande en annan. 

Hrmm undra just hur en sådan databas skulle se ut. 

Elev
----
*id
förnamn
efternamn
gatuadress
telefonnummer
-klassid

Klass
----
*id
klassnamn

Sal
----
*id
salsnamn
hus

Ämne
----
*id
ämnesnamn
beskrivning

Lärare
----
*id
förnamn
efternamn
huvudämne

Lektion
----
*id
-Lärarid
-Ämnesid
-Salsid
-Elevid
starttid
sluttid

**Uppgift**
Skapa databasen
Lägg in data i alla tabeller. Se till att du har tillräckligt med elever för 5 olika lektioner. 
Ha gärna lektioner vid samma tidpunkt men med olika lärare och elever etc.

Plocka ut schemat för en elev under en dag. 
Plocka ut Schemat för en klass för en dag. 
Tag fram alla lektioner som en lärare har på en vecka. 

