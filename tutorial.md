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
Når battlebot får tallet 0 fra fjernkontrollen skal den stoppe. Vi kan da bruke blokken ``||DF-Driver:Motor stop all||`` fra kategorien DF-Driver.

```blocks
radio.onReceivedNumber(function (receivedNumber) {
    if (receivedNumber == 0) {
        motor.motorStopAll()
    } else {
    	
    }
})
```

### Steg 5
Vi legger så inn nye sammenligningsblokker for verdiene 1 og 2 - fremover og bakover.   
Hent to blokker av ``||DF-Driver:Motor M1 dir CW speed||`` fra kategorien DF-Driver. Plasser begge blokkene under hvis receivedNumber = 1. Endre den ene blokken slik at den sier ``||DF-Driver:Motor M2 dir CW speed||``
Her må dere velge rotasjon som stemmer med motorene slik de er montert på deres battlebot. CW står for ClockWise og CCW CounterClockWise.   
Motorene kan være montert slik at de går i motsatt retning selv om det i koden står CW på både motor 1 og 2. Gjør nødvendige endringer i programmet slik at det blir riktig for dere.

```blocks
radio.onReceivedNumber(function (receivedNumber) {
    if (receivedNumber == 0) {
        motor.motorStopAll()
    } else if (receivedNumber == 1) {
        motor.MotorRun(motor.Motors.M1, motor.Dir.CW, 150)
        motor.MotorRun(motor.Motors.M2, motor.Dir.CW, 150)
    } else if (receivedNumber == 2) {
        motor.MotorRun(motor.Motors.M1, motor.Dir.CCW, 150)
        motor.MotorRun(motor.Motors.M2, motor.Dir.CCW, 150)
    } else{    	
    }
})
```

### Steg 6
Vi legger så inn nye sammenligningsblokker for verdiene 3 og 4 - snu til venstre og snu til høyre.
Hent inn to motorblokker for hver verdi. Legg nå merke til at motorene settes til å gå motsatt retning av hverandre. Her vil det være mulig å justere hvor fort battleboten spinner ved å endre på hastigheten til en eller begge motorene. 
```blocks
radio.onReceivedNumber(function (receivedNumber) {
    if (receivedNumber == 0) {
        motor.motorStopAll()
    } else if (receivedNumber == 1) {
        motor.MotorRun(motor.Motors.M1, motor.Dir.CW, 150)
        motor.MotorRun(motor.Motors.M2, motor.Dir.CCW, 150)
    } else if (receivedNumber == 2) {
        motor.MotorRun(motor.Motors.M1, motor.Dir.CCW, 150)
        motor.MotorRun(motor.Motors.M2, motor.Dir.CW, 150)
    } else if (receivedNumber == 3) {
        motor.MotorRun(motor.Motors.M1, motor.Dir.CCW, 70)
        motor.MotorRun(motor.Motors.M2, motor.Dir.CCW, 150)
    } else if (receivedNumber == 4) {
        motor.MotorRun(motor.Motors.M1, motor.Dir.CW, 150)
        motor.MotorRun(motor.Motors.M2, motor.Dir.CW, 70)
    }
})
```
### Steg 7

Sett radiogruppe. For at fjernkontroll og battlebot skal kunne motta signaler fra hverandre må begge microbit være i samme radiogruppe.   
Hent ``||radio:sett radiogruppe||`` fra radio og sett gruppenummere til det samme som dere valgte i fjernkontrollprogrammet.

```blocks
radio.setGroup(xx)
```

```package
DF-Driver=github:DFRobot/pxt-motor
``` 