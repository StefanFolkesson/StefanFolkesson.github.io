# Hantera Events i react
Ett event i react måste vara passiv och inte kallas på direkt. 
exempel:
```JSX
{//(korrekt)
}
<button onClick={handleEvent}>

{//(fel)
}
<button onClick={handelEvent()}>
```
Skillnaden är liten men ack så viktig. Du vill att eventet skall kallas på när du trycker på knappen inte när du laddar sidan.

Detta leter till att du även behöver använda en anonym funktion när du skall kalla på en annan funktion med indata.
exempel:
```JSX
{//(korrekt)
}
<button onClick={() => alert('du är här')}>

{//(fel)
}
<button onClick={alert('du är här')}>

```
Igen om du inte använder en anonym funktion så kommer alerten köras varje gång sidan renderas. 

Så:
onClick={handleEvent} skickar dig till funktionen när du klickar.
onClick={() => alert('du är här')} kör den anonyma funktionen när du klickar.  

