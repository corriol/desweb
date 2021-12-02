# Activitats

## Cookies

### Projecte MovieFX 

501. Última visita. 

    Modifica la pàgina `index.php` de forma que emmagatzeme en una galleta l'últim instant en què l'usuari va visitar la pàgina. 

    Si és la seva primera visita, mostra un missatge de benvinguda. En cas contrari, mostra la data i hora de la seva anterior visita. 

    La galleta tindrà una durada d'una setmana.

    Comprova que la galleta s'ha creat correctament.


502. Emmagatzematge del nom de l'usuari.

     L'objectiu és que quan un usuari inicie sessió s'emmagatzeme el nom introduït en un galleta, de forma que quan torne a accedir al formulari d'inici de sessió aparega el nom automàticament.

     El nom de la _cookie_ serà `last_used_name` i la durada serà de 30 dies.
     
     Crea la pàgina `logout.php` que en accedir eliminarà la _cookie_.

503. Assegurant les galetes.

     Després de llegir l'article enllaçat, aplica els canvis oportuns per a fer més segures les _cookies_.

## Maneig de sessions

### Projecte MovieFX

504. Registre de visites

    Modifica la pàgina inicial del projecte de forma que s'emmagatzeme en la sessió d'usuari els instants de totes les seves últimes visites. Si és la seva primera visita, mostra un missatge de benvinguda. En cas contrari, mostra la data i hora de totes les seves visites anteriors. Afegeix un botó a la pàgina que permeti esborrar el registre de visites.

505. Control d'accés
     
     Utilitza també una variable de sessió per a comprovar si l'usuari ja ha iniciat sessió correctament. D'aquesta manera no caldrà comprovar les credencials amb la base de dades constantment.

506. Evitar atacts CSRF

    Implementa en el formulari de creació de pel·lícules la solució proposada en els apunts.

507. Gestió de formularis en dos fitxers.

    Modifica el formulari de creació de pel·lícules de forma que es gestione en dos fitxers tal com s'indica en els apunts.

508. Bones pràctiques

    Adapta el projecte de forma que:

     1.  Cada 15 minuts es regenere la sessió.
     2.   Sols use http per accedir a la _cookie_ de sessió.
     3.   Les constrasenyes s'encripten amb _bcrypt_.
     4.   Es tanque la sessió tal com s'indica.