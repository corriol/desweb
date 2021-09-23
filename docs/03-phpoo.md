# Programació Orientada a Objectes en PHP

## Introducció

La programació orientada a objectes (OOP, per les seues sigles en
anglès) és un paradigma de programació.

Paradigma:

> Teoria […] el nucli central de la qual \[…\] suministra la base i el
> model per resoldre problemes i avançar en el coneixement.

Per la qual cosa podem definir la programació orientada a objecte com
un mètode -provat i estudiat- el qual es basa en les interaccions
d'objectes per resoldre les necessitats d'un sistema informàtic.

Un objecte és una estructura que conté dades i el codi que els maneja.

L'estructura dels objectes es defineix en les classes. En elles s'escriu
el codi que defineix el comportament dels objectes i s'indiquen els
membres que formaran part dels objectes d'aquesta classe. Entre els
membres de una classe pot haver-hi:

  - **Mètodes**. Són els membres de la classe que contenen el codi de la
    mateixa. Un mètode és com una funció. Pot rebre paràmetres i
    retornar valors.
  - **Atributs o propietats**. Emmagatzemen informació sobre el estat de
    l'objecte al que pertanyen (i per tant, el seu valor pot ser
    diferent per a cadascun dels objectes de la mateixa classe).

A la creació de un objecte basat en una classe se li anomena instanciar
una classe i a l'objecte obtingut també se li coneix com a instància
d'aqueixa classe.

Els pilars fonamentals de la POO són:

  - **Herència**. És el procés de crear una classe a partir de una altra,
    heretant el seu comportament i característiques i podent
    redefinir-los.
  - **Abstracció**. Fa referència al fet que cada classe oculta en el seu
    interior les peculiaritats de la seua implementació, i presenta a
    l'exterior una sèrie de mètodes (interfície) el comportament dels
    quals està ben definit. Vist des de l'exterior, cada objecte és un
    ens abstracte que realitza un treball.
  - **Polimorfisme**. Un mateix mètode pot tenir comportaments diferents en
    funció de l'objecte amb que s'utilitze.
  - **Encapsulació**. En la POO s'ajunten en un mateix lloc les dades i el
    codi que els manipula.

Els avantatges més importants que aporta la programació orientada a
objectes són:

  - **Modularitat**. La POO permet dividir els programes en parts o
    mòduls més xicotets, que són independents uns d'uns altres però
    poden comunicar-se entre ells.
  - **Extensibilitat**. Si es desitgen afegir noves característiques a
    una aplicació, la POO facilita aquesta tasca de dues formes: afegint
    nous mètodes al codi, o creant nous objectes que estenguen el
    comportament dels ja existents.
  - **Manteniment**. Els programes desenvolupats utilitzant POO són més
    senzills de mantenir, a causa de la modularitat abans comentada.
    També ajuda seguir certes convencions en escriure'ls , per exemple,
    escriure cada classe en un fitxer propi. No ha d'haver-hi dues
    classes en un mateix fitxer, ni un altre codi a part de el propi de
    la classe.
    
## Característiques bàsiques de l'ús d'objectes en PHP

### Introducció
Segurament tot, o la majoria del que acabes de veure, ja ho coneixies,
i és fins i tot probable que sàpigues utilitzar algun llenguatge de
programació orientat a objectes, així que anem a veure directament les
peculiaritats pròpies de PHP en el que fa referència a la POO.

En PHP podemos utilitzar els dos paradigmes de la programació: estructurada i orientada a objectes.

```php
 // utilitzant programació estructurada
$dwes = mysqli_connect('localhost', 'dwes', 'abc123.', 'dwes');
// utilizant POO
$dwes = new mysqli();
$dwes->connect('localhost', 'dwes', 'abc123.', 'dwes');
```

No obstant açò, el llenguatge PHP original no es va dissenyar amb
característiques d'orientació a objectes. Només a partir de la versió 3,
es van començar a introduir alguns trets de POO en el llenguatge. Açò es
va potenciar en la versió 4, encara que encara de forma molt
rudimentària. Per exemple, en PHP4:

  - Els objectes es passen sempre per valor, no per referència.
  - No es pot definir el nivell d'accés per als membres de la classe.
    Tots són públics.
  - No existeixen les interfícies.
  - No existeixen mètodes destructors.

En PHP5 es va reescriure i potenciar el suport d'orientació a objectes del llenguatge, ampliant les seues
característiques i millorant el seu rendiment i el seu funcionament general. Les característiques de POO que 
suporta PHP5 inclouen:

  - Mètodes estàtics.
  - Mètodes constructors i destructors.
  - Herència.
  - Interfícies.
  - Classes abstractes.

Entre les característiques que no inclou PHP5, i que pots conèixer
d'altres llenguatges de programació, estan:

  - Herència múltiple.
  - Sobrecàrrega de mètodes (tenir diversos mètodes amb el mateix nom,
    però amb funcionalitats diferents. Els mètodes sobrecarregats han de
    tenir diferents paràmetres. Quan es diu al mètode, s'utilitza una o
    una altra versió en funció dels paràmetres amb que es realitze la
    trucada (podent distingir per el seu nombre i per el seu tipus,
    segons el llenguatge de programació utilitzat)) (inclosos els
    mètodes constructors).
  - Sobrecàrrega d'operadors (similar a la sobrecàrrega de mètodes. Es
    poden definir diverses funcionalitats a un mateix operador, i
    s'utilitzarà una o una altra en funció del tipus dels operands que
    s'usen en cada instant).

PHP 7 incorpora millores en el rendiment i el tipat d'arguments, valors de retorn i atributs (des de la versió 7.4)

### Definició de classes

La declaració de una classe en PHP es fa utilitzant la paraula `class`. A continuació i entre claus, han de 
figurar els membres de la classe.

Convé fer-ho de forma ordenada, primer les propietats o atributs, i
després els mètodes, cadascun amb el seu codi respectiu.

```php
class Product {
    private string $code;
    public string $name;
    public float $price;
    public function show() {
        print "<p>" . $this->code . "</p>";
    }
}
```
Com comentàvem abans, és preferible que cada classe figure en el seu
propi fitxer (**`Product.php`**). A més, molts programadors prefereixen
utilitzar per a les classes noms que comencen per lletra majúscula, per
a, d'aquesta forma, distingir-los dels objectes i altres variables.

Una vegada definida la classe, podem usar la paraula **`new`** per a
instanciar objectes de la següent forma:

```php
$product = new Product();
```

Perquè la línia anterior s'execute sense error, prèviament hem d'haver
declarat la classe. Per a açò, en aqueix mateix fitxer hauràs de
incloure la classe posant alguna cosa com:

```php
require('Product.php');
```

Els atributs de una classe són similars a les variables de PHP. És
possible indicar un valor en la declaració de la classe. En aquest cas,
tots els objectes que s'instancien a partir de aqueixa classe, partiran
amb aqueix valor per defecte en l'atribut.

Per a accedir des d'un objecte als seus atributs o als mètodes de
la classe, has d'utilitzar l'operador fletxa (fixa't que només es posa
el símbol $ davant del nom de l'objecte):

```php
$product->name = 'Samsung Galaxy S';
$product->show();
```

Quan es declara una propietat o un mètode, s'ha d'indicar el seu nivell d'accés (o visibilitat). Els
principals nivells són:

  - `public`. Els atributs declarats com `public` poden utilitzar-se
    directament per els objectes de la classe. És el cas de l'atribut
    `$name` anterior.
  - `private`. Els atributs declarats com `private` només poden ser
    accedits i modificats per els mètodes definits en la classe, no
    directament per els objectes de la mateixa. És el cas de l'atribut
    `$code`.
  - `protected`. Una propietat o mètode `protected` sols pot ser accedida per la classe on es defineix o per un subclasse. No és accessible des de fora.  


Un dels motius per a crear atributs privats és que el seu valor forma
part de la informació interna de l'objecte i no ha de formar part de la
seua interfície. Un altre motiu és mantenir cert control sobre els seus
possibles valors. Per exemple, si no vols que es puga canviar lliurement
el valor del codi d'un producte. O necessites conèixer quin serà el nou
valor abans d'assignar-lo. En aquests casos, se solen definir aqueixos
atributs com a privats i a més es creen dins de la classe mètodes per a
permetre'ns obtenir i/o modificar els valors d'aqueixos atributs. Per
exemple:

```php
private $code;
public function setCode($newCode) {
    if (!existsCode($newCode)) {
        $this->code = $newCode;
        return true;
    }
    return false;
}
public function getCode() { return $this->code; }
```

Encara que no és obligatori, el nom del mètode que ens permet obtenir el
valor de un atribut sol començar per `get`, i el que ens permet
modificar-lo per `set`.

En PHP5 es van introduir els anomenats mètodes màgics, entre ells
`__set` i `__get`. Si es declaren aquests dos mètodes en una classe, PHP
els invoca automàticament quan des de un objecte s'intenta usar un
atribut no existent o no accessible. Per exemple, el codi següent simula
que la classe `Product` té qualsevol atribut que vulguem usar.

```php
class Product {
    private $atributos = array();
    public function __get($atributo) {
        return $this->atributos[$atributo];
    }
    public function __set($atributo, $valor) {
        $this->atributos[$atributo] = $valor;
    }
}
```

### Constructor i destructor

Com ja has vist, per a instanciar objectes de una classe s'utilitza la
paraula `new`:

```php
$product = new Product();
```

En PHP7 pots definir en les classes mètodes constructors, que s'executen
quan es crea l'objecte.

El constructor d'una classe ha d'anomenar-se `__construct`. Es poden utilitzar, per exemple, 
per assignar valors a atributs.

```php
class Product {
    private static $numProducts = 0;
    private $code;
    public function __construct()
    {
        self::$numPoducts++;
    }
    …
}
```

El constructor d'una classe pot cridar a altres mètodes o tenir
paràmetres, en aquest cas hauran de passar-se quan es crea l'objecte.
No obstant açò, només pot haver-hi un mètode constructor en cada classe.

```php
class Product {
    private static $numProducts = 0;
    private $code;
    public function __construct($code) {
        $this->$code = $code;
        self::$numProducts++;
    }
    ...
}
$p = new Product('GALAXYS');

```

Per exemple, si com en aquest exemple, definim un constructor en el qual
calga passar el codi, sempre que instancies un nou objecte d'aqueixa
classe hauràs de indicar el seu codi.

També és possible definir un mètode destructor, que ha d'anomenar-se
`__destruct()` que s'executarà quan s'elimine l'objecte.

```php

class Product {
private static $numProducts = 0;
    private $code;
    public function __construct($code) {
        $this->$code = $code;
        self::$numProducts++;
    }
    public function __destruct() {
        self::$numProducts--;
    }
    ...
}
$p = new Product('GALAXYS');

```

### La pseuodovariable $this

Quan des d'un objecte s'invoca un mètode de la classe, a aquest se li
passa sempre una referència a l'objecte que ha fet la crida. Aquesta
referència s'emmagatzema en la pseudovariable `$this.` S'utilitza, per
exemple, en el codi anterior per a tenir accés als atributs privats de
l'objecte (que només són accessibles des dels mètodes de la classe).

```html+php
echo "<p>" . $this->code . "</p>";
```

En la documentació de PHP tens més informació sobre els mètodes màgics:
<http://es.php.net/manual/es/language.oop5.magic.php>

### Constants de classe

A més de mètodes i propietats, en una classe també es poden definir constants, 
utilitzant la paraula `const`. És important que no confongues els atributs amb
les constants. Són conceptes diferents: les constants no poden canviar el seu 
valor (òbviament, de ací el seu nom), no usen el caràcter `$`, s'escriuen en 
majúscules (per convenció)  i el seu valor està associat a la classe, és a dir, 
no existeix una còpia del mateix en cada objecte. 

Per tant, per a accedir a les constants d'una classe, s'ha d'utilitzar el 
nom de la classe i l'operador `::`, anomenat operador de resolució d'àmbit 
(que s'utilitza per a accedir a els elements de una classe).

```php
class DB {
    const USUARIO = 'dwes';
      ...
}
echo DB::USUARIO;
```

És important ressaltar que no és necessari que existisca cap objecte de
una classe per a poder accedir al valor de les constants que definisca.
 
### PHP Standard Recommendations

!!! important "PHP-FIG"
    El PHP Framework Interop Group és un grup de treball on està involucrada gent que treballa en diferents _frameworks_ amb
    l'objectiu de posar en comú les tècniques que usen en els diferents projectes per poder integrar-les i compartir-les 
    i poder treballar millor junts.

Les recomanacions [PSR-1](https://www.php-fig.org/psr/psr-1/) i [PSR-12](https://www.php-fig.org/psr/psr-12/) 
són recomanacions sobre l'estil de programació amb l'objectiu d'aplicar estandards comuns i 
així facilitar la lectura del codi realitzar per altres.

Algunes recomancions que cal seguir:

1.  Class names MUST be declared in `StudlyCaps`. For instance: `Product`.
2.  Class constants MUST be declared in all upper case with underscore separators. For example: const IMAGE_PATH.      
3.  About property names the only recommendation is to be consistent. So, we SHOULD use `$camelCase`. The same recommendations applies for variables.
4.  Method names MUST be declared in `camelCase()`.

Més informació en [Estándares](http://coppeldev.github.io/php/standards/psr-1.html)


### Mètodes o atributs estàtics

Tampoc s'han de confondre les constants amb els membres estàtics d'una
classe. En PHP7, una classe pot tenir atributs o mètodes estàtics, també
anomenats a vegades atributs o mètodes de classe. Es defineixen utilitzant
la paraula clau `static`.

```php
class Product {
    private static $numProducts = 0;
    public static function newProduct() {
        self::$numProducts++;
    }
       …
}
```

Els atributs i mètodes estàtics no poden ser cridats des d'un objecte de
la classe utilitzant l'operador `->`. Si el mètode o atribut és públic,
haurà d'accedir-se utilitzant el nom de la classe i l'operador de
resolució d'àmbit.

```php
Product::newProduct();
```

Si és privat, com l'atribut `$numProducts` en l'exemple anterior,
només es podrà accedir a ell des dels mètodes de la pròpia classe,
utilitzant la paraula `self`. De la mateixa forma que `$this` referencia
a l'objecte actual, `self` fa referència a la classe actual.

```php
self::$numProductes++;
```

Els atributs estàtics d'una classe s'utilitzen per a guardar informació general sobre la mateixa, com pot ser 
el nombre d'objectes que s'han instanciat. Només existeix un valor de l'atribut, que s'emmagatzema a
nivell de classe.

Els mètodes estàtics solen realitzar alguna tasca específica o retornar un objecte concret. Per exemple, 
les classes matemàtiques solen tenir mètodes estàtics per a realitzar logaritmes o arrels quadrades. No té
sentit crear un objecte si l'única cosa que volem és realitzar una operació matemàtica.

Els mètodes estàtics es criden des de la classe. No és possible
cridar-los des d'un objecte i per tant, no podem usar `$this` dins d'un
mètode estàtic.

### Utilització d'objectes

Ja saps com instanciar un objecte utilitzant `new`, i com accedir a els
seus mètodes i atributs públics amb l'operador fletxa:

```php
$product = new Product();
$product->name= 'Samsung Galaxy S';
$product->show();
```

Una vegada creat un objecte, pots utilitzar l'operador `instanceof` per
a comprovar si és o no una instància de una classe determinada.

```php
if ($product instanceof Product) {
        …
}
```

Des de PHP7, pots indicar en les funcions i mètodes de quina classe han
de ser els objectes que es passen com a paràmetres. Per a açò, has
d'especificar el tipus abans del paràmetre.

```php
public function sellProduct(Product $product) {
    …
}
```

Si quan es realitza la crida, el paràmetre no és del tipus adequat, es
produeix un error que podries capturar. 

Una característica de la POO que has de tenir molt en compte és què
succeeix amb els objectes quan els passes a una funció, o simplement
quan executes un codi com el següent:

```php
$p = new Product();
$p->name = 'Samsung Galaxy S';
$a = $p;
```

El codi anterior simplement crearia un nou identificador del mateix objecte. Açò és,
quan s'utilitze qualsevol dels identificadors per a canviar el valor de algun atribut, aquest canvi es 
veuria també reflectit en accedir utilitzant l'altre identificador. Recorda que, encara que hi haja dos o
més identificadors del mateix objecte, en realitat tots es refereixen a l'única còpia que s'emmagatzema 
del mateix.

Per tant, a partir de PHP5 no pots copiar un objecte utilitzant
l'operador `=`. Si necessites copiar un objecte, has d'utilitzar `clone`. En
utilitzar `clone` sobre un objecte existent, es crea una còpia del mateix.

A més, existeix una forma senzilla de personalitzar la còpia per a cada
classe particular. Per exemple, pot succeir que vulgues copiar tots els
atributs menys algun. En el nostre exemple, almenys el codi de cada
producte ha de ser diferent i, per tant, potser no tinga sentit
copiar-lo en crear un nou objecte. Si aquest fóra el cas, pots crear un
mètode de nom `__clone` en la classe. Aquest mètode es cridarà
automàticament després de copiar tots els atributs en el nou objecte.

### Comparació d'Objectes

En utilitzar l'operador de comparació (==), es comparen d'una manera
senzilla les variables de cada objecte, és a dir: dues instàncies d'un
objecte són iguals si tenen els mateixos atributs i valors (els valors
es comparen amb ==), i són instàncies de la mateixa classe.

Quan s'utilitza l'operador identitat (===), les variables d'un objecte
són idèntiques si i només sí fan referència a la mateixa instància de
la mateixa classe.

### Clonació d'Objectes

Per crear una còpia d'un objecte s'utilitza la paraula clau `clone` (que
invoca, si fos possible, al mètode  `__clone()` de l'objecte). No es pot
cridar el mètode `__clone()` d'un objecte directament.

```php
$copia_objecte = clone $objecte;
```

Quan es clona un objecte, PHP7 durà a terme una còpia superficial de les
propietats de l'objecte. Les propietats que siguen referències a altres
variables (per exemple, objectes), mantindran les referències.

Compte: si els atributs són objectes no es clonaran.

### Iteració d'objectes

PHP 7 ofereix una forma de definir objectes, de manera que és possible
recórrer una llista d'elements amb, per exemple, una sentència `foreach`.
Per defecte, s'utilitzaran totes les propietats visibles per a la
iteració.

## Herència
### Introducció

L'herència és un mecanisme de la POO que ens permet definir noves
classes sobre la base d'una altra ja existent. Les noves classes que
hereten també es coneixen amb el nom de subclasses. La classe de la qual
hereten es diu classe base o superclasse.

Per exemple, en la nostra tenda web anem a tenir productes de diferents
tipus. En principi hem creat per a manejar-los una classe anomenada
`Product`, amb alguns atributs i un mètode que genera una eixida
personalitzada en format HTML del codi.

```php
class Product {
   public string $code;
   public string $name;    
       
   public function show() {
      echo "<p>" . $this->code . "</p>";
   }
}
```

Aquesta classe és molt útil si l'única informació que tenim dels
diferents productes és la que es mostra a dalt. Però, si vols
personalitzar la informació que vas a tractar de cada tipus de producte
(i emmagatzemar, per exemple per als televisors, les polzades que tenen
o la seua tecnologia de fabricació), pots crear noves classes que
hereten de `Product`. Per exemple, `TV`, `Computer`, `Phone`.

```php
class TV extends Product {
    public $size;
    public $technology;
}
```

### La paraula reservada `extends`

Com pots veure, per a definir una classe que herete d'una altra,
simplement has de utilitzar la paraula `extends` indicant la superclasse. 

Els nous objectes que s'instancien a partir de la subclasse 
són també objectes de la classe base; es pot comprovar utilitzant l'operador `instanceof`.

```php
$tv = new TV();
if ($tv instanceof Product) {
  // Aquest codi s'executa doncs la condició és certa
        …
}
```

La nova classe hereta tots els atributs i mètodes públics de la classe
base, però no els privats. Si vols crear en la classe base un mètode no
visible a l'exterior (com els privats) que s'herete a les subclasses,
has d'utilitzar la paraula **protected** en lloc de **private**. A més, pots
redefinir el comportament dels mètodes existents en la classe base,
simplement creant en la subclasse un nou mètode amb el mateix nom.

```php
class TV extends Producte { 
   public $size;
   public $technology;
        
   public function show() {
      print "<p>" . $this->size . " polzades</p>";
   }
}
```

## La paraula reservada `final`

Existeix una forma d'evitar que les classes heretades puguen redefinir
el comportament dels mètodes existents en la superclasse: utilitzar la
paraula `final`.

Si en el nostre exemple haguérem fet:

```php
class Product { 
    public $code; 
    public $name;         
    public $price;
    
    public final function show() {
        print "<p>" . $this->code . "</p>";
    }
}
```

En aquest cas el mètode `show` no podria redefinir-se en la classe `TV`.

També es pot declarar una classe utilitzant `final`. En aquest cas no
podran crear-se classes heretades utilitzant-les com a base.

```php
final class Product {
  ...
}
```

### La paraula reservada `abstract`

Oposadament al modificador `final`, existeix també `abstract`.

S'utilitza de la mateixa forma, tant amb mètodes com amb classes
completes, però en lloc de prohibir l'herència, obliga a que s'herete.
És a dir,  una classe amb el modificador abstract no pot tenir objectes que la
instancien, però sí podrà utilitzar-se de classe base i les seues
subclasses sí podran utilitzar-se per a instanciar objectes.

```php
abstract class Product {
   ...
}
```

Un mètode en el qual s'indique `abstract`, ha de ser redefinit obligatòriament per les subclasses, i no 
podrà contenir codi.

```php
class Product {
        …
    abstract public function show();
}
```

Anem a fer una petita modificació en la nostra classe `Product`. Per a
facilitar la creació de nous objectes, crearem un constructor al que se
li passarà un array amb els valors dels atributs del nou producte.

```php
class Product {
    public $code;
    public $name;
    public $shortName;
    public $price;
    
    public function show() {
        echo "<p>" . $this->code . "</p>";
    }
    public function __construct($row) {
        $this->code = $row['code'];
        $this->name = $row['name'];
        $this->shortName = $row['short_name'];
        $this->price = $row['price'];
    }
}
```

**Què passa ara amb la classe `TV`, què hereta de Product? Quan crees un
nou objecte d'aqueixa classe, es cridarà al constructor de Product?
Pots crear un nou constructor específic perquè redefinisca el
comportament de la classe base?**

Començant per aquesta última pregunta, òbviament pots definir un nou
constructor per a les classes heretades que redefinisquen el
comportament del que existeix en la classe base, tal com faries amb
qualsevol altre mètode. I depenent de si programes o no el constructor
en la classe heretada, es cridarà o no automàticament al constructor de
la classe base.

En PHP5+, si la classe heretada no té constructor propi, es cridarà
automàticament al constructor de la classe base (si existeix). No
obstant açò, si la classe heretada defineix el seu propi constructor,
hauràs de ser tu el que realitze la crida al constructor de la classe
base si ho consideres necessari, utilitzant per a açò la paraula
`parent` i l'operador de resolució d'àmbit.

```php
class TV extends Product {
    public $size;
    public $technology;
    
    public function show() {
        print "<p>" . $this->size . " polzades</p>";
    }
    
    public function __construct($row) {
        parent::__construct($row);
        $this->size = $row['size'];
        $this->technology = $row['technology'];
    }
 }
```

Ja has vist amb amb anterioritat com s'utilitzava la paraula clau `self`
per a tenir accés a la classe actual. La paraula `parent` és semblant. En
utilitzar `parent` fas referència a la classe base de la actual, tal com
apareix rere `extends`.


## Interfícies


### Introducció

Un interfície (*interface*) és com una classe buida que solament conté declaracions de mètodes. 
Es defineixen utilitzant la paraula `interface`. Per exemple, abans vam veure que podíem crear noves classes
heretades de `Product`, com `TV` o `Ordinador`. També vam veure que en les subclasses
podies redefinir el comportament del mètode perquè generara una eixida
en HTML diferent per a cada tipus de producte.

Si vols assegurar-te que tots els tipus de productes tinguen un mètode
`show`, pots crear un interface com el següent.

```php
interface IShow {
    public function show();
}
```

I quan crees les subclasses hauràs d'indicar amb la paraula `implements`
que han de implementar els mètodes declarats en aquest interface.

```php
class TV extends Product implements IShow {
            …
    public function show() {
        echo "<p>" . $this->size . " polzades</p>";
    }
        …
}
```

Tots els mètodes que es declaren en un `interface` han de ser públics. A
més de mètodes, els interfícies podran contenir constants però no
atributs.

Un interface és com un contracte que la classe ha de complir. En
implementar tots els mètodes declarats en la interfície s'assegura la
interoperabilitat entre classes. Si saps que una classe implementa un
interfície determinada saps quins noms tenen els seus mètodes, quins
paràmetres els has de passar i, probablement, podràs esbrinar fàcilment
amb quins objectiu han sigut escrits.

Per exemple, en la llibreria de PHP està definit la interfície
`countable`.

```php
Countable {
    abstract public int count ( void )
}
```

Si crees una classe per a la cistella de la compra en la tenda web,
podries implementar aquesta interfície per a contar els productes que
figuren en la mateixa.

Abans vas aprendre que en PHP5 una classe només pot heretar d'una altra.
En PHP5 no existeix l'herència múltiple. No obstant açò, sí és possible
crear classes que implementen diverses interfícies, simplement separant
la llista d'interfícies per comes després de la paraula `implements`.

```php

class TV extends Product implements IShow, Countable {
         …
}
```

L'única restricció és que els noms dels mètodes que s'hagen
d'implementar en els diferents interfícies no coincidisquen. És a dir,
en el nostre exemple, la interfície `IShow` no podria contenir el
mètode `count`, doncs aquest ja està declarat en `Countable`.

En PHP7 també es poden crear nous interfícies heretant d'uns altres ja
existents. Es fa de la mateixa forma que amb les classes, utilitzant la
paraula `extends`.

## Classes abstractes vs interfícies

Un dels dubtes més comuns en POO, és quina solució adoptar en algunes
situacions: interfícies o classes abstractes. Ambdues permeten definir
regles per a les classes que els implementen o hereten respectivament. I
cap permet instanciar objectes. Les diferències principals entre ambdues
opcions són:

  - En les classes abstractes, els mètodes poden contenir codi. Si van a
    existir diverses subclasses amb un comportament comú, es podria
    programar en els mètodes de la classe abstracta. Si s'opta per un
    interface, caldria repetir el codi en totes les classes que ho
    implemente.
  - Les classes abstractes poden contenir atributs, i les interfícies
    no.
  - No es pot crear una classe que herete de dues classes abstractes,
    però sí es pot crear una classe que implemente diverses interfícies.

Per exemple, en la botiga *online* va a haver-hi dos tipus d'usuaris:
clients i empleats. Si necessites crear en la teua aplicació objectes de
tipus Usuari (per exemple, per a manejar de forma conjunta als
clients i als empleats), hauries de crear una classe no abstracta amb
aqueix nom, de la qual heretarien Client i Empleat.

Podeu llegir també l'article
 [Clases abastractas e interfaces en PHP ](https://poesiabinaria.net/2010/06/clases-abstractas-e-interfaces-en-php/)


```php
class Usuari {
     ...
}
class Client extends Usuari {
...
}
class Empleat extends Usuari {
...
}

```

Però si no fóra així, hauries de decidir si crees o no `Usuari`, i si ho
faries com una classe abstracta o com una interfície.

Si per exemple, volgueres definir en un únic lloc els atributs comuns a
Client i a Empleat, hauries de crear una classe abstracta Usuari de la
qual hereten.

```php
abstract class Usuari {
    public $dni;
    
    protected $nom;
        ...
}
```

Però açò no podries fer-ho si ja tens planificada alguna relació
d'herència per a una d'aquestes dues classes.

Per a finalitzar amb les interfícies, a la llista de funcions de PHP
relacionades amb la POO pots afegir les següents.

| Funció                     | Exemple                                  | Significat                                                                  |
| -------------------------- | ---------------------------------------- | --------------------------------------------------------------------------- |
| get\_declared\_interfícies | print\_r (get\_declared\_interfícies()); | Retorna un array amb els noms dels interfícies declarats.                   |
| interface\_exists          | if (interface\_exists('iShow') { … }  | Retorna true si existeix l'interface que s'indica, o false en cas contrari. |


{:.alert .alert-activity}
<div markdown="1">




## Trets (Traits)



Des de la seva versió 5.4.0, PHP implementa una metodologia de
reutilització de codi anomenada `Traits`.


Els trets («traits» en anglès) són un mecanisme de reutilització de
codi en llenguatges d'herència simple, com PHP. L'objectiu d'un tret és
el de reduir les limitacions pròpies de l'herència simple permetent que
els desenvolupadors reutilitzen a voluntat conjunts de mètodes sobre
diverses classes independents i pertanyents a classes jeràrquiques
diferents. 

Un Trait és similar a una classe, però amb l'únic objectiu d'agrupar
funcionalitats molt específiques i d'una manera coherent. No es pot
instanciar directament un `Trait`. És per tant un afegit a l'herència
tradicional, i habilita la composició horitzontal de comportaments; és a
dir, permet combinar membres de classes sense haver d'usar herència.

```php   
trait Saludar {
    function decirHola(){
        return "hola";
    }
}
trait Despedir {
    function decirAdios(){
        return "adiós";
    }
}
class Comunicacion {
    use Saludar, Despedir;
}
$comunicacion = new Comunicacion;
echo $comunicacion->decirHola() . ", que tal. " . $comunicacion->decirAdios();
```

En l'exemple anterior la classe `Comunicacion` necessita reutilitzar els mètodes `Saludar::decirHola()` i 
`Despedir::decirAdios()` com que en PHP no hi ha herència múltiple mitjançant els `trait` es pot aconseguir 
reutilitzar-les.

## Gestió d'errors i excepcions


### Introducció
De ben segur que a mesura que has anat resolent exercicis o simplement
provant codi, t'has trobat amb errors de programació. Alguns són
reconeguts per l'entorn de desenvolupament i pots corregir-los abans
d'executar. Altres apareixen al navegador en forma de missatge d'error a
l'executar l'*script*.

A diferència d'altres llenguatges de programació que tenen una gestió d'excepcions
més completa PHP manté una gestió d'excepcions lleugera ja que distingeix entre errors i excepcions. 
Així mentre no es produisca una excepció o un error fatal l'execució del programa continua.

No obstant, en PHP 7 canvia la majoria dels errors notificats per PHP. En lloc de notificar errors a través 
de l'mecanisme de notificació d'errors tradicional de PHP 5, la majoria dels errors ara són
 notificats llançant excepcions `Error`.

A l'igual que les excepcions normals, les excepcions `Error` es propagaran fins a arribar al
primer bloc `catch` coincident. Si no hi ha blocs coincidents, serà invocat qualsevol 
gestor d'excepcions predeterminat instal·lat amb `set_exception_handler ()`, i si no hi hagués 
cap gestor d'excepcions predeterminat, l'excepció serà convertida en un error fatal i serà manejada 
com un error tradicional.

A causa de que la jerarquia d'`Error` no hereta de `Exception`, el codi que empre blocs catch 
(Exception $ e) {...} per gestionar excepcions no capturades en PHP 5 trobareu que 
aquests `Errors` no són capturats per aquests blocs. Es requereix, per tant, un bloc 
`catch (Error $i)` {...} o un gestor `set_exception_handler()`.

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
{:.no_toc .nocount }

```ini
; PHP comes packaged with two INI files. One that is recommended to be used
; in production environments and one that is recommended to be used in
; development environments.

; php.ini-production contains settings which hold security, performance and
; best practices at its core. But please be aware, these settings may break
; compatibility with older or less security conscience applications. We
; recommending using the production ini in production and testing environments.
```
```ini
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
</div>


### Gestió global dels errors
En utilitzar la funció `error_reporting` només controles quin tipus
d'errors va a notificar PHP. A vegades pot ser suficient, però per
obtenir més control sobre el procés existeix també la possibilitat de
gestionar de forma personalitzada els errors. És a dir, pots programar
una funció perquè siga la que executa PHP cada vegada que es produeix un
error. El nom d'aquesta funció s'indica utilitzant `set_error_handler` i
ha de tenir com a mínim dos paràmetres obligatoris (el nivell de l'error
i el missatge descriptiu) i fins tres opcionals amb informació addicional 
sobre el error (el nom del fitxer en què es produeix, el
nombre de línia, i un bolcat de l'estat de les  
variables en aquest moment).

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

  - `PDO::ERRMODE\_SILENT`. No es fa res quan ocorre un error. És el
    comportament per defecte.
  - `PDO::ERRMODE\_WARNING`. Genera un error de tipus E\_WARNING quan es
    produeix un error.
  - `PDO::ERRMODE\_EXCEPTION`. Quan es produeix un error llança una
    excepció utilitzant el gestor propi PDOException.

És a dir, que si vols utilitzar excepcions amb l'extensió PDO, has de
configurar la connexió fent:

```php
$dwes-> setAttribute (PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
```

Per exemple, el següent codi:
```php
    $dwes = new PDO ( "mysql: host = localhost; dbname = dwes", "dwes", "abc123.");
    $dwes-> setAttribute (PDO :: ATTR_ERRMODE, PDO :: ERRMODE_EXCEPTION);
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
    echo "No es pot posar un ID negatiu\n";
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