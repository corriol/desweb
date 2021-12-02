# Gestió d'errors i excepcions

De ben segur que a mesura que has anat resolent exercicis o simplement
provant codi, t'has trobat amb errors de programació. Alguns són
reconeguts per l'entorn de desenvolupament i pots corregir-los abans
d'executar. Altres apareixen al navegador en forma de missatge d'error a
l'executar l'*script*.

A diferència d'altres llenguatges de programació que tenen una gestió d'excepcions
més completa PHP manté una gestió d'excepcions lleugera ja que distingeix entre errors i excepcions. 
Així, mentre no es produisca una excepció o un error fatal l'execució del programa continuarà.

No obstant això, en PHP 7 canvia la majoria dels errors notificats per PHP. En lloc de notificar errors a través 
de l'mecanisme de notificació d'errors tradicional de PHP 5, la majoria dels errors ara són
 notificats llançant excepcions `Error`.

A l'igual que les excepcions normals, les excepcions `Error` es propagaran fins a arribar al
primer bloc `catch` coincident. Si no hi ha blocs coincidents, serà invocat qualsevol 
gestor d'excepcions predeterminat definit amb `set_exception_handler ()`, i si no hi hagués 
cap gestor d'excepcions predeterminat, l'excepció serà convertida en un error fatal i serà gestionada 
com un error tradicional.

A causa de que la jerarquia d'`Error` no hereta de `Exception`, el codi que empre blocs `catch 
(Exception $e) {...}` per gestionar excepcions no capturades en PHP 5 trobareu que 
aquests `Errors` no són capturats per aquests blocs. Es requereix, per tant, un bloc 
`catch (Error $e) {...}` o un gestor `set_exception_handler()`.

## Errors
PHP defineix una classificació dels errors que es poden produir en
l'execució d'un programa i ofereix mètodes per ajustar el tractament
dels mateixos. Per fer referència a cada un dels nivells d'error, PHP
defineix una sèrie de constants. Cada nivell s'identifica per una
constant. Per exemple, la constant `E_NOTICE` fa referència a avisos que
poden indicar un error en executar el programa, i la constant `E_ERROR`
engloba errors fatals que provoquen que s'interrompa forçosament l'execució.

La llista completa de constants la pots consultar al manual de PHP, on
també es descriu el tipus d'errors que representa :
[http://es.php.net/manual/es/errorfunc.constants.php](http://es.php.net/manual/es/errorfunc.constants.php)

### Canviar el comportament de PHP 
La configuració inicial de com va a tractar-se cada error segons el seu
nivell es realitza en `php.ini` el fitxer de configuració de PHP. Entre
els principals paràmetres que pots ajustar estan:

  - `error_reporting`. Indica quins tipus d'errors es notificaran. El
    seu valor es forma utilitzant els operadors a nivell de bit per
    combinar les constants anteriors. El seu valor per defecte és `E_ALL
    & ~ E_NOTICE` que indica que es notifiquin tots els errors (`E_ALL`)
    excepte els avisos a temps d'execució (`E_NOTICE`).
  - `display_errors`. En el seu valor per defecte (`On`), fa que els
    missatges s'envien a la sortida estàndard (i per tant es mostrin al
    navegador). S'ha de desactivar (`Off`) en els servidors que s'usen per 
    a producció.

Hi ha altres paràmetres que podem utilitzar en `php.ini` per ajustar el
comportament de PHP quan es produeix un error.
<http://es.php.net/manual/es/errorfunc.configuration.php>

Des codi, pots fer servir la funció `error_reporting` amb les constants
anteriors per establir el nivell de notificació en un moment determinat.
Per exemple, si en algun lloc del teu codi figura una divisió en la qual
hi haja la possibilitat que el divisor siga zero, quan això passe
obtindràs un missatge d'error al navegador. Per evitar-ho, pots
desactivar la notificació de errors de nivell `E_WARNING` abans de la
divisió i restaurar al seu valor normal a continuació:

```php
error_reporting(E_ALL & ~ E_NOTICE & ~ E_WARNING);
$resultat = $dividend/$divisor;
error_reporting (E_ALL & ~ E_NOTICE);
```

### Notificació d'error en entorns de producció
```ini
; PHP comes packaged with two INI files. One that is recommended to be used
; in production environments and one that is recommended to be used in
; development environments.
; php.ini-production contains settings which hold security, performance and
; best practices at its core. But please be aware, these settings may break
; compatibility with older or less security conscience applications. We
; recommending using the production ini in production and testing environments.

; display_errors
;   Default Value: On
;   Development Value: On
;   Production Value: Off

; display_startup_errors
;   Default Value: Off
;   Development Value: On
;   Production Value: Off

; error_reporting
;   Default Value: E_ALL & ~E_NOTICE & ~E_STRICT & ~E_DEPRECATED
;   Development Value: E_ALL
;   Production Value: E_ALL & ~E_DEPRECATED & ~E_STRICT

; html_errors
;   Default Value: On
;   Development Value: On
;   Production value: On

; log_errors
;   Default Value: Off
;   Development Value: On
;   Production Value: On
```

### Gestió global dels errors
En utilitzar la funció `error_reporting` només controles quin tipus
d'errors va a notificar PHP. A vegades pot ser suficient, però per
obtenir més control sobre el procés existeix també la possibilitat de
gestionar de forma personalitzada els errors. És a dir, pots programar
una funció perquè siga la que executa PHP cada vegada que es produeix un
error. El nom d'aquesta funció s'indica utilitzant `set_error_handler` i
ha de tenir com a mínim dos paràmetres obligatoris (el nivell de l'error
i el missatge descriptiu) i fins tres opcionals amb informació addicional 
sobre el error (el nom del fitxer en què es produeix, el nombre de línia, 
i un bolcat de l'estat de les variables en aquest moment).

```php
set_error_handler ("miGestorDeErrores");
$resultat = $dividend / $divisor;
restore_error_handler ();
function miGestorDeErrores ($nivell, $missatge)
{
    switch ($nivell) {
        case E_WARNING:
          echo "Error de tipus WARNING: $missatge. <br />";
          break;
        default:
          echo "Error de tipus no especificat: $ missatge. <br />";
    }
}
```

La funció `restore_error_handler` restaura el gestor d'errors original
de PHP (més concretament, el que s'estava fent servir abans de la crida
a `set_error_handler`).

### ErrorException

Gràcies a la combinació de la classe `ErrorException` i el mètode `set_error_handler` 
podem convertir fàcilment els errors en excepcions de tipus `ErrorException`:

```php
<?php
function exception_error_handler($severidad, $mensaje, $fichero, $línea) {
    if (!(error_reporting() & $severidad)) {
        // Este código de error no está incluido en error_reporting
        return;
    }
    throw new ErrorException($mensaje, 0, $severidad, $fichero, $línea);
}
set_error_handler("exception_error_handler");

/* Desencadenar la excepción */
strpos();
?>
```

## Excepcions

A partir de la versió 5 es va introduir en PHP un model d'excepcions
similar a l'existent en altres llenguatges de programació:

  - El codi susceptible de produir algun error s'introdueix en un bloc
    `try`.
  - Quan es produeix algun error, es llança una excepció utilitzant la
    instrucció `throw`.
  - Després del bloc `try` ha d'haver com a mínim un bloc `catch`
    encarregat de processar el error.
  - Si un cop acabat el bloc `try` no s'ha llançat cap excepció, es
    continua amb la execució en la línia següent al bloc o blocs
    `catch`.

Per exemple, per llançar una excepció quan es produeix una divisió per
zero podries fer:

```php
try {
   if ($divisor == 0)
      throw new Exception ( "Divisió per zero.");
   $resultat = $dividend/$divisor;
}
catch (Exception $e) {
   echo "S'ha produït el següent error:". $ e-> getMessage ();
}
```

PHP ofereix una classe base `Exception` per utilitzar com a gestor
d'excepcions. Per llançar una excepció no cal indicar cap paràmetre,
encara que de forma opcional es pot passar un missatge d'error (com en
l'exemple anterior) i també un codi d'error.

Entre els mètodes que podeu utilitzar amb els objectes de la classe
`Exception` estan:

  - `getMessage`. Retorna el missatge, en cas que s'hagi posat algun.
  - `getCode`. Retorna el codi d'error si existeix.

Les funcions internes de PHP i moltes extensions com MySQLi usen el
sistema d'errors vist anteriorment. Només les extensions més modernes
orientades a objectes, com és el cas de PDO, utilitzen aquest model
d'excepcions. En aquest cas, el més comú és que l'extensió definisca els
seues propis controladors d'errors heretant de la classe `Exception`.

!!! information "Classe ErrorException"
    Com hem dit abans, utilitzant la classe `ErrorException` és possible traduir els errors a
    excepcions.[http://es.php.net/manual/es/class.errorexception.php](http://es.php.net/manual/es/class.errorexception.php)

Concretament, la classe PDO permet definir la fórmula que farà servir
quan es produeixi un error, utilitzant l'atribut `PDO::ATTR_ERRMODE`.
Les possibilitats són:

  - `PDO::ERRMODE_SILENT`. No es fa res quan ocorre un error. És el
    comportament per defecte.
  - `PDO::ERRMODE_WARNING`. Genera un error de tipus E\_WARNING quan es
    produeix un error.
  - `PDO::ERRMODE_EXCEPTION`. Quan es produeix un error llança una
    excepció utilitzant el gestor propi PDOException.

És a dir, que si vols utilitzar excepcions amb l'extensió PDO, has de
configurar la connexió fent:

```php
$dwes-> setAttribute (PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
```

Per exemple, el següent codi:
```php
    $dwes = new PDO("mysql:host=localhost;dbname=dwes", "dwes", "abc123.");
    $dwes-> setAttribute (PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
    try {
        $sql = "SELECT * FROM stox";
        $result = $dwes->query ($sql);
        ...
    }
    catch (PDOException $p) {
        echo "Error". $p-> getMessage (). "<br />";
    }
```

Captura l'excepció que llança PDO a causa de que la taula no existeix.
El bloc `catch` mostra el següent missatge:

```php
Error SQLSTATE [42S02]: Base table or view not found: 1146 Table 'dwes.stox' does not exist
```

### El bloc `finally`

En PHP 5.5 i posterior, es pot utilitzar un bloc `finally` després o en
lloc dels blocs `catch`. El codi de dins el bloc `finally` sempre
s'executarà després dels blocs `try` i `catch`, independentment que
s'haja llançat una excepció o no, i abans que l'execució normal
continue.

Com que el contingut del bloc `finally` sempre s'executa és ideal per a
alliberar recursos en cas d'error, com una connexió a base de dades o a
la connexió a un servei proporcionats per tercers.`  `

### Múltiples catch

És possible afegir més d'un `cath` de la següent manera:

```php
try {
   ...
} catch (FooException e) {
   ...
} catch (BarException e) {
   ...
} catch (Exception e) {
   ...   
}
```

A partir de PHP 7.1 també és possible fer-ho així:

```php
try {
   ...
} catch (FooException | BarException | Exception e) {
   ...
}
```

## Ampliant les excepcions

És possible crear excepcions personalitzades heretant de la classe
`Exception`.

```php
class NegativeIdException extends Exception {
  public function __construct($message = null) {
    $this->message = $message ?: 'ID Negatiu.';
    parent::__construct($message);
  }
}
```

Després l'utilitzarem així:

```php
try {
  $post = new Post(-1, "Hola món", "Aquest és el primer post del blog", new DateTime(), "Vicent");
} catch (NegativeIdException $e) {
    echo "No es pot posar un ID negatiu";
} catch (Exception $e) {
  echo "Excepció desconeguda".  $e->getMessage();
}
```

## Interfície Throwable
_Throwable_ és la interfície base per a qualsevol objecte que puga ser llançat 
mitjançant una sentència `throw` en PHP 7, incloent `Error` i `Exception`.

Les classes de PHP no poden implementar la interfície `Throwable` directament, 
de manera que han d'estendre en el seu lloc `Exception`.

Aquesta nova interfície té per objectiu unificar les dos tipologies d'exceptions. Tant `Exception` com 
`Error` implementen la interfície `Throwable`. 


### Gestió d'errors i excepcions

1.  Modifica les classes Input creades anteriorment perquè en cas que
    el atribut `$name` no tinga valor llance una excepció amb el missatge
    "L'atribut name no pot estar buit".
2.  Captura l'excepció.
3.  Crea una excepció personalitzada `ValuesNotFoundException` en cas
    que el paràmetre `$values` del control `InputRadio` estiga buit.
4.  Captura l'excepció.
5.  Crea una excepció personalitzada `MovieNotFound` que es llance
    en cas que l'identificador `$id` sol·licitat no trobe cap pel·licula en `single-page.php`      
6.  Captura l'excepció.

## Exercicis pràctics

### Activitat: Pel·lícules

#### Objectius
Els objectius de l'activitat són els següents:
* Aprendre a crear classes
* Instanciar objectes
* Accedir a les seues propietats.

#### Enunciat
1. Crea la classe Movie en la carpeta src del projecte (**cal usar tipat esctricte**).
2. Els atributs seran:
    * id (enter)
    * title (string)
    * tagline (string)
    * releaseDate (DateTime)
    * starsRating (float)
    * poster (string)
3. Crea els _setters_ i els _getters_.
4. La constant de classe `POSTER_PATH` contindrà la ruta al directori dels posters.
5. Modifica el projecte de forma que `$movies` siga un array d’objectes `Movie`.
6. Modifica'l també perquè les pàgines index.php i movies.php funcionen correctament


### Activitat: Pel·licules II


#### Objectius
Els objectius de l'activitat són els següents:
* Repassar el concepte de paràmetres per referència.
* Clonar objectes.

#### Enunciat

1. Crea una pel·lícula copiant-la (=) de la darrera pel·lícula de l'array.  
2. Comprova en movies.php que s'ha insertat i que tenen les mateixes dades.
3. Ara canvia el títol de la còpia afegint-li "(Còpia)" al títol que tenía. Per exemple si el títol era "Ava" ara serà 
"Ava (còpia)".
4. Comprova en `movies.php` que s'ha insertat i que és diferent a l'original. Tenen les mateixes dades? Per què?
5. Repassa els apunts i soluciona-ho. 

### Activitat: Pel·lícules III

#### Objectius
Els objectius de l'activitat són els següents:
* Seguir construint el projecte.
* Treballar amb objectes.

#### Enunciat
1. El títol de la pel·licula  serà un enllaç a `single-page.php?id=[atribut id de la pel·lícula]`.
2. La pàgina `single-page.php` mostrarà les dades de la pel·licula que tinga l'`id` que s'ha passat pel 
querystring.
3. Post usar `array_filter` per trobar l'objecte que té l'id indicat.

### Activitat 4.2: Herència

#### Objectius

Els objectius de l'activitat són els següents:
* Treballar l'herència.
* Treballar amb classes abstractes

#### Enunciat


Anem a crear una sèrie de classes per mostrar camps de formulari.

Pots incloure'ls al projecte en `src/utils` o crear-les a banda en la carpeta `activitat4` en 
l'arrel del projecte.

Crea la classe abstracta `Input` que tindrà les propietats:
* **title**, serà el text que apareix com a etiqueta de camp.
* **name**, serà el atribut name del camp.
* **value**, serà el valor a mostrar si hi ha.
* **type** , serà el tipus de camp, el valor per defecte serà 'text' i es modificarà
internament en les subclasses (`$this->type=??`).

El constructor serà 
```php
public function __construct(string $title, string $name, string $value);
```

Tindrà un mètode `generateHTML()` que no tindrà paràmetres i tornarà un string amb
l'HTML que representa el camp.

Per exemple:
```html
<label>Nom</label>
<input type="text" value=""  name="nom" />
```

A continuació crea les classes `InputText`, `InputEmail` (_type=email_), `InputTel`(_type=tel_), 
 que hereten de la classe abstracta i usa-les per a crear un formulari en els camps
 * Nom
 * Cogonms
 * Correu electrònic
 * Telèfon fixe
 * Telèfon mòbil.
 * Enviar (pots implementar la classe `InputSubmit` o escriure'l directament en HTML.
 
 La pàgina de resposta mostrarà els valors enviats pel formulari. 


### Activitat 4.3: Herència (i 2)
{:.no_toc .nocount}

#### Objectius
{:.no_toc .nocount}
Els objectius de l'activitat són els següents:
* Treballar l'herència.
* Treballar amb classes abstractes
* Treballar el polimorfisme

#### Enunciat
{:.no_toc .nocount}

Anem a crear una sèrie de classes per mostrar camps de formulari.

Pots incloure'ls al projecte en `src/utils` o crear-les a banda en la carpeta `activitat4` en 
l'arrel del projecte.

Crea les classes `InputRange` i `InputRadio` que heretaran de la classe abstracta però que
tindran el constructor i els atributs diferents. Afig als camps ja existents els camps:
 
 * Edat (de tipus range, 40 serà el valor per defecte)
 * Sexe (de tipus radio amb el sexe)
  

Crea la classe `Form` que representarà un formulari HTML.  

El constructor serà 
```php
public function __construct(string $action, string $method ='POST');
```

Tindrà una propietat pública `$elements` que serà un array d'objectes `Input`. Un mètode `Form::add(Input $input)`
que afegirà elements a l'array.

Tindrà també altres dos mètodes `Form::generateStartHTML()` que generarà l'etiqueta `<form...>` i 
`Form::generaEndHTML()` que generarà l'etiqueta de tancament `</form>`

Crea un objecte `Form` i afig mitjançant el mètode `add` els elements ja existents i mostra el formulari.
 
La pàgina de resposta mostrarà els valors enviats pel formulari.
 


### Activitat 4.4: Interfície IControl

#### Objectius

Els objectius de l'activitat són els següents:
* Crear interfícies.
* Treballar amb classes abstractes
* Treballar el polimorfisme

#### Enunciat
{:.no_toc .nocount}

Crea una nova classe `Textarea` semblant a la classe `Input` que generarà 
un camp textarea de formulari. 

Podrem afegir objectes `Textarea` mitjançant el mètode `Form::add()`?;

Crea la interfície `IControl`:

```php
interface IControl {
    public function render(): string;
}
```
Totes les classes creades implementaran eixa interfície.

Modifica `Form::add()` perquè admeta paràmetres de tipus `IControl`.

Implementa en la classe `Form` la interfície `Countable`. 

Després mitjançant la funció `count()` mostra el número total d'elements del formulari.

## Bibliografia
{: .no_toc }

  - José Luis Comesaña.  *Apuntes de formación a distancia del módulo
    «Desarrollo web en entorno servidor» del CFGS DAW, elaborados y
    licenciados por el Ministerio de Educación, Cultura y Deporte.* \[en
    línia\]. 2012 \[data de consulta: 13 de setembre de 2019\].
    Disponible en
    \<<https://github.com/statickidz/TemarioDAW/tree/master/DWES>\>
  - Antonio López. *Learning PHP 7.* Packt Publishing (29 de marzo de
    2016) .