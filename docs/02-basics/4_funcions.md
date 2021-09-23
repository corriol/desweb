
# 4. Funcions

## Funcions predefinides

Algunes de les funcions predefinides en PHP són les següents, però hi ha moltíssimes més 
vinculades als diferents mòduls que podem instal·lar.

* **is_null($var)** determina si una variable és nula o no.
* **isset($var)** determina si una variable estan definida i no és NULL.
* **unset($var)** destrueix les variables especificades.
* **empty($var)** torna **true** si no existeix o és **FALSE**
* **is_int($var)**, **is_float()**, **is_bool()**, **is_array()**
* **var_dump($var)** mostra informació de la variable.

## Funcions definides per l'usuari

Per a crear les teues pròpies funcions, hauràs d'usar la paraula **function**:

```php
function suma($a, $b) 
{ 
	return $a + $b; 
}
```

Per tal d'invocar la funció:

```php
$resultat = suma(5, 7);
```

Si una funció no té una sentència **return**, retorna **null** en finalitzar.

## Valors per defecte en els paràmetres

* Podem indicar valors per defecte per als paràmetres. Si quan cridem a la funció no indiquem el valor d'un paràmetre es prendrà el valor per defecte indicat.

```php
function preuAmbIva($preu, $iva=0.21){
	return $preu * (1 + $iva);
}
$preu = 10;
$pIva = preuAmbIva($preu);
```

* Pot haver-hi més d'un paràmetre amb valor per defecte, però sempre han d'estar al final.

## Pas de paràmetres per referència

Per defecte els paràmetres es passen per valor. Per a passar un paràmetre per referència afegirem el símbol **&** davant del seu nom.

```php
function preuAmbIva(&$preu, $iva=0.18){
	$preu *= (1 + $iva);
}
```

#### Declaracions de tipus (Type Hinting)

Les funcions obliguen a que els paràmetres siguen de cert tipus. Si el valor donat és d'un tipus incorrecte, es generarà un error. Per això s'ha d'anteposar-se el nom del tipus al nom del paràmetre. Es pot fer que una declaració accepte valors **NULL** si el valor predeterminat del
paràmetre s'estableix a NULL.

#### Tipus vàlids
| Type | Description | Version |
|:---:|:---:|:---:|
|Class/interface name |The value must be an instanceof the given class or interface. ||
|self|The value must be an instanceof the same class as the one in which the type declaration is used. Can only be used in classes.||
|parent|The value must be an instanceof the parent of the class in which the type declaration is used. Can only be used in classes.||
|array|The value must be an array.||
|callable|The value must be a valid callable. Cannot be used as a class property type declaration.||
|bool|The value must be a boolean value.||
|float|The value must be a floating point number.||
|int|The value must be an integer.||
|string|The value must be a string.||
|iterable|The value must be either an array or an instanceof Traversable.| PHP 7.1.0 |
|object|The value must be an object.|PHP 7.2.0|
|mixed|The value can be any value.|PHP 8.0.0|

#### Exemple

```php
function suma(int a, int b):int
{
	return $a + $b;
}
$resultado = suma(3,5);
```

#### Funcions com a paràmetres

En PHP és possible passar funcions com a paràmetres a altres funcions. Només cal passar el nom de la funció entre cometes. 
Exemple:

```php
 function calculator($operation,$numA,$numB){
	return $operation($numA,$numB); 
}
function sumar($a,$b) { return $a+$b; }
function restar($a,$b) {return $a-$b; }

$a=4;$b=6;
echo calculator('sumar',$a,$b);
echo calculator('restar',$a,$b);
```

#### Funcions anònimes (**closures**)

* Estan implementades usant la classe **Closure**
* Permeten la creació de funcions que no tenen un nom específic
* Podem assignar la funció a una variable o passar-la com a paràmetre a una altra funció.
* Exemple
  
Sense paràmetres:

```php
$anonima = function () {
	echo "Hola"; 
}; 
$anonima();
```

Amb paràmetres:

```php
$anonima = function ($nom) {
	echo "Hola {$nom}"; 
}; 
$anonima('Vicent');
```

#### Usar variables de l'àmbit superior

* Una funció anònima pot usar variables de l'àmbit superior mitjançant la paraula reservada **use**: 

```php
function saluda(callable $fnSaluda) {
	$fnSaluda('Vicent'); 
} 
$salutacio = 'Hola'; 
$anonima = function ($nom) use ($salutacio) {
	echo "{$salutacio} {$nom}"; 
}; 
saluda($anonima);
```

#### Llibreries

Podem fer llibreries de funcions guardant-les en un fitxer que desprès importem des d'on les utilitzem. Ho podem fer amb include, o utilitzant composer per a fer-ho.

### Activitat 241: funció imatge

Crea el fitxer funcions.php

Escriviu una funció per retornar una etiqueta HTML `<img />`. 

La funció hauria d’acceptar com a argument obligatori l’URL de la imatge i arguments opcionals per a un text 
alternatiu, alçada i amplada.

### Activitat 242: funció imatge local

Copieu la funció de l’exercici anterior i modifiqueu-la de manera que només es passe el nom de fitxer a la funció en
 lloc de l’URL completa. Dins de la funció, farem ús d’una variable global per fer l’URL completa.
  
Per exemple, si passem `photo.png` a la funció, i la variable global conté `/images`, llavors l’atribut `src` de 
l'etiqueta <img> retornada serà `/images/photo.png`. 

Una funció com aquesta és una forma senzilla de mantenir correctes les vostres etiquetes d’imatges, fins i tot si les
 imatges es mouen a un nou camí o servidor. Només cal canviar la variable global, per exemple, de `/images` a 
 `http://images.example.com/.`


### Activitat 243: Funcions

Els colors web com `#ffffff` i `#cc3399` es realitzen concatenant els valors hexadecimals de color per a vermell, 
verd i blau. 

Escriu una funció que accepte 3 arguments: roig, verd i blau, i que retorne un string que conté el color adequat per
 utilitzar-lo en una pàgina web. 

Per exemple, si els arguments són 255, 0, i 255, llavors la cadena retornada hauria de ser #FF00FF.
 
Pot resultar útil utilitzeu la funció `dechex()` integrada, que es troba documentada a [http://www.php.net/](http://www.php.net/)

Assegureu-vos que els paràmetres reben valors enters i que són colors vàlids.

Implementa 3 exemples d’ús.


### Activitat 244: SQL

Crea un fitxer anomenat `funcions_sql.php`.

Crea una funció anomenada `insert`  que ens genere una sentència INSERT INTO en SQL.  

Per a açò la funció rebrà dos paràmetres:  
1. El nom de la taula  
2. Un array associatiu que contindrà els noms i valors dels camps de la taula.
 
La sentència resultant tindrà la següent forma: 

```
“INSERT INTO nom_taula (nom dels camps separats per comes) VALUES (noms dels camps separats per comes amb el caràcter “:” davant)  
```
De moment, no farem res amb els valors dels camps. 

Ajuda: utilitza les funcions `sprintf`, `implode` i `array_keys`

### Activitat 245: SQL 

A partir de l'exercici anterior crea una altra funció que reba els mateixos paràmetres més un paràmetre booleà 
per a indicar si volem generar la query amb els noms dels camps o no. 

El paràmetre tindrà el valor `true` per defecte.
 
Si el seu valor és `true` generarà la consulta igual que en l'exercici anterior, però si és `false` la generarà així: 

```sql
INSERT INTO nom_taula 
  VALUES (valors dels camps separats per comes amb el caràcter ‘:’ davant)
```


### Activitat 246: SQL 

Repeteix l'exercici anterior amb els següents canvis: 

La cadena resultant es passarà per referència.

Passarem la cadena de la següent forma: 

```sql
INSERT INTO taula (camps) VALUES (valors) 
```

Dins de la funció substituirem el següent: 

1. El text taula pel nom de la taula. 
2. El text camps pels noms dels camps separats per comes
3. El text valors pels noms dels camps separats per comes i el caràcter ‘:’ davant. 

