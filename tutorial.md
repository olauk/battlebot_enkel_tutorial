### @activities 1

## Battlebot - programmering av mottakerprogram

### Programmer mottakerprogram til enkel fjernkontroll @unplugged
Vi skal nå programmere mottakerprogrammet som sammen med enkel fjernkontroll styrer battleboten vår.   
Det er en fordel om dere allerede har laget programmet "enkel fjernkontroll" for vi skal i dette programmet bestemme hva battleboten gjør når den mottar de ulike tallene fra fjernkontrollen.

Vi må huske hvilke verdier vi har programmert fjernkontrollen til å sende. (Tallene under er standardverdiene i tutorialen)     
__Knapp A__ - styrer battleboten _fremover_   - sender tallet __1__ via radio   
__Knapp B__ - styrer battleboten _bakover_  - sender tallet __2__ via radio   
__Roll__ - styrer om battleboten svinger til _høyre_ eller _venstre_  - sender tallet __3__ eller tallet __4__ via radio   
__Knapp A+B__ - stopper battleboten - sender tallet __0__ via radio   

## Motta signaler

### Steg 1
Når microbit mottar radiosignaler fra fjernkontrollen må vi tolke disse. For å gjøre det bruker man _vilkår_   
Hent ``||radio:Når radio mottar receivedNumber||`` fra kategorien radio. Hent ``||logic:Hvis ellers||`` fra logikk og plasser den i ``||radio:Når radio mottar recivedNumber||``
```blocks
radio.onReceivedNumber(function (receivedNumber) {
    if (true) {
    	
    } else {
    	
    }
})
```

### Steg 2

Vi må undersøke hvilken verdi microbit har fått fra fjernkontrollen. Tall som mottas via radio lagres i _receivedNumber_ helt til en ny verdi kommer via radio. Her må dere bruke de tallene dere brukte i deres fjernkontrollprogram.    
For å undersøke hvilken verdi receivedNumber har bruker vi sammenligningsblokken fra logikk og plasserer den i _Hvis ellers_.   
Trekk så ut den røde _receivedNumber_ og plasser den i den første ruten i sammenligningsblokken slik at det står Hvis receivedNumber = 0.

```blocks
radio.onReceivedNumber(function (receivedNumber) {
    if (receivedNumber == 0) {
    	
    } else {
    	
    }
})
```

### Steg 3

Hent to blokker av ``||DF-Driver:Motor M1 dir CW speed||`` fra kategorien DF-Driver. Plasser begge blokkene under hvis receivedNumber = 0. Endre den ene blokken slik at den sier ``||DF-Driver:Motor M2 dir CW speed||``

```blocks
radio.onReceivedNumber(function (receivedNumber) {
    if (receivedNumber == 0) {
        motor.MotorRun(motor.Motors.M1, motor.Dir.CW, 0)
        motor.MotorRun(motor.Motors.M2, motor.Dir.CW, 0)
    } else {
    	
    }
})
```

### Steg 5
Vi skal nå gjøre det samme for å snu til høyre:   
Hent ``||input:når ristes||`` fra inndata. Endre denne til ``||input:når helning høyre||`` Hent ``||radio:radio send tall||`` fra radio. Velg selv hvilket tall som skal bety snu til høyre.

```blocks
input.onGesture(Gesture.TiltLeft, function () {
    radio.sendNumber(3)
})
input.onGesture(Gesture.TiltRight, function () {
    radio.sendNumber(4)
})
```

### Stopp @unplugged
Det er lurt å ha en mulighet for å stoppe battleboten.
Dette kan gjøres på ulike måter. Vi viser her hvordan dere kan gjøre det ved å bruke ``||input:når knapp A trykkes||``

### Steg 6
Hent ``||input:når knapp A trykkes||`` fra inndata. Hent ``||radio:radio send tall||`` fra radio. Velg selv hvilket tall som skal bety stopp.
```blocks
input.onButtonPressed(Button.AB, function () {
    radio.sendNumber(0)
})
```

```package
DF-Driver=github:DFRobot/pxt-motor
``` 