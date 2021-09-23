# 1. Programació web amb PHP

## PHP

* Acrònim de _Personal Home Page_
* Llenguatge de propòsit general, encara que el seu fort és el desenvolupament web.
* Sintaxi similar a C / Java
* El codi s'executa en el servidor (en Apache mitjançant _mod_php_)
* El client rep el resultat generat després d'interpretar el codi al servidor.
* El codi s'emmagatzema en arxiu amb extensió `.php.`

L'última versió és la 8.0, de novembre de 2020 (i en breu tindrem la versió 8.1). La versió 7.0 va sortir al desembre de 2015. A més de nombroses noves funcionalitats que anirem veient durant el curs, té més de dues vegades millor rendiment que PHP5.

La seva documentació és extensa i està traduïda: https://www.php.net/manual/es/. 

## Funcionament i estructura bàsica
### El nostre primer codi PHP 

* El codi PHP sempre va entre els simbolos `<?php` i `?>`.
* Les instruccions PHP acaben sempre amb `;`.
* Per a generar codi HTML des de PHP podem utilitzar el mètode `echo` passant-li el text del codi que volem generar.
* El codi pot anar entre les etiquetes d'HTML.

```html+php
<html>
<head></head>
<body>
	<h1><?php echo "Hola món" ?></h1>
<body>
```

* També podem utilitzar l'etiqueta **<?=** fa el echo al mateix temps.

```html+php
<html>
<head></head>
<body>
	<h1><?= "Hola món" ?></h1>
<body>
```

### Comentaris

* De bloc entre `/*` i `*/`.
* De linea, començant per `//` o per `#`.

### Codi incrustat

El documents que contenen codi PHP s'han d'anomenar amb l'extensió **.php**

## Variables i tipus de dades

Una de les característiques de php és que és un llenguatge **no fortament tipat**. 
De fet no cal declarar la variable ni indicar el tipus de dades si la declare. 
Encara que si volem codi de qualitat ho hauriem de fer.

#### Declaració 

* Els noms de les variables sempre comencen per `$` 
* Després del $ els noms de les variables han d'anar seguits per una lletra o el caràcter `_` i poden contenir també números. 
* No és necessari declarar una variable ni especificar-li un tipus (sencer, cadena,...) concret.

Per crear una variable que continga el text a generar i mostrar-la:

```html+php
<html>
<head></head>
<body>
	<h1>
	<?php 
		$salutacio = "Hola món";
		echo $salutacio; 
	?>
	</h1>
<body>
```

#### Tipus de les variables

* El tipus de la variable es decideix en funció del context en què s'utilitze.
* En assignar-li el valor 7, la variable és de tipus “sencer” 

```php
$la_meua_variable = 7;  // ara és un número
$la_meua_variable = "set"; // ara és cadena
```

Si li canviem el contingut passa a ser de tipus “cadena”

##### Variable no inicialitzades

Si s'intenta utilitzar una variable abans d'assignar-li un valor, es genera un error de tipus **E_NOTICE** però no s'interromp l'execució de l'script. L'eixida mostrarà un avís cada volta que s'intente.
 
#### Tipus de dades en PHP

* booleà (**boolean**). Els seus possibles valors són true i false. A més, qualsevol nombre enter es considera com true, excepte el 0 que és false.
* sencer (**integer**). Qualsevol nombre sense decimals. Es poden representar en format decimal, octal (començant per un 0), o hexadecimal (començant per 0x).
* real (**float**). Qualsevol nombre amb decimals. Es poden representar també en notació científica.
* cadena (**string**). Conjunts de caràcters delimitats per cometes simples o dobles.
* vector (**array**). Conjunt de variables del mateix tipus ordenades.
* Objecte (**object**). Utilitzat per les instàncies de classes.
* **null**. És un tipus de dades especial, que s'usa per a indicar que la variable no té valor. (<http://php.net/manual/es/language.types.null.php>)

#### Àmbit de les variables

L'àmbit d'una variable és la part del codi en que és visible. 
Una variable declarada en un fitxer de PHP està disponible en eixe fitxer i en els que l'incloguen. 
Les funcions definixen un àmbit local, separat de la resta del codi.
Es poden definir variables globlals amb la paraula reservada **global**, encara que no són aconsellables.

#### Variables predefinides
Són variables internes predefinides de PHP que poden usar-se des de qualsevol àmbit. Tomem forma **d'arrays associatius** que contenen un conjunt de valors.

  * **$_SERVER**. Conté informació sobre l'entorn del servidor web i d'execució.
  * **$_GET, $_POST i $_COOKIE** contenen les variables que s'han passat al
script actual utilitzant, respectivament, els mètodes GET (paràmetres en la URL), HTTP POST i Cookies HTTP 
  * **$_REQUEST** junta en un solament el contingut dels tres *arrays anteriors,
$_GET, $_POST i $_COOKIE. 
  * **$_ENV** conté les variables que es puguen haver passat a PHP des de l'entorn en què s'executa. 
  * **$_FILES** conté els fitxers que es puguen haver pujat al servidor
utilitzant el mètode POST. 
  * **$_SESSION** conté les variables de sessió disponibles per al guió
actual.

<http://es.php.net/manual/es/language.variables.superglobals.php>

## Constants

Per a definir constants s'utilitza **define()**, que reb el nom de la constant i el valor que li volem donar

```php
define("LIMITE",1000);
```

És habitual utilitzar identificadors en majuscules per a les constants.

## Operadors  

### Arimètics

| Exemple | Nom | Resultat
| ---   | ---   | ---
| `+$a` | Identidat | Conversió de `$a` a `int` o `float` segons el cas.
| `-$a` | Negació | Oposat de `$a`.
| `$a + $b` | Suma | Suma de `$a` i `$b`.
| `$a - $b` | Resta | Diferència de `$a` i `$b`.
| `$a * $b` | Multiplicació | Producte de `$a` i `$b`.
| `$a / $b` | Divisió | Quocient de `$a` i `$b`.
| `$a % $b` | Módul / Residu | Residu de `$a` dividit per `$b`.
| `$a ** $b` | Potència | Resultat de `$a` elevat a `$b`. PHP >= 5.6.

En el caso de **cadenas**, si queremos concatenarlas, se utiliza el operador `.`:

```php
$x = 33;
$y = 11;
$z = $x + $y;
echo "La suma de 33 y 11 es ".44."<br />";
echo "La suma de ".$x." y ".$y." es ".(33 + 11)."<br />";
echo "La suma de ".$x." y ".$y." es ".$z."<br />";
```

Realment en lloc de concatenar cadenas con variables, podem imprimir-les directament 
ja que s'expandeixen automàticament:

``` php
echo "La suma de $x y $y es $z <br />";
```

En ocasions, necesitem envoltar el nom de la variable entre claus per poder un més text al resultat:

``` php
$color = "rojo";
echo "El plural de $color el ${color}s";
?>
```

Més endavant estudiarem algunes funcions per al tractament de cadenes.

### Comparació

| Exemple | Nom | Resultat
| ---   | ---   | ---
| `$a == $b` | Igual | `true` si `$a` és igual a `$b` després de la conversió de tipus.
| `$a === $b` | Idèntic, Comparació estricta | `true` si `$a` és igual a `$b`, i són del mateix tipus de dada.
| `$a != $b`, `$a <> $b` | Diferent |`true` si `$a` no és igual a `$b` després de la conversió de tipus.
| `$a !== $b` | No idèntic |`true` si `$a` no és igual a `$b`, o si no són del mateix tipus.
| `$a < $b` | Menor que |`true` si `$a` és estrictament menor que `$b`.
| `$a > $b` | Major que |`true` si `$a` és estrictament major que `$b`.
| `$a <= $b` | Menor o igual que |`true` si `$a` és menor o igual que `$b`.
| `$a >= $b` | Major o igual que |`true` si `$a` és major o igual que `$b`.
| `$a <=> $b` | Nau espacial | Torna `-1`, `0` o `1` quan `$a` és respectivamente menor, igual, o major que `$b`. PHP >= 7.
| `$a ?? $b ?? $c` | Fusión de *null* | El primer operano d'esquerra a dreta que existisca i no siga `null`. `null` si no hi ha valors definits i no són `null`. PHP >= 7.

### Lògics

| Exemple | Nom | Resultat
| ---   | ---   | ---
| `$a and $b`, `$a && $b` | *And* (i) | `true` si tant `$a` com `$b` són `true`.
| `$a or $b`, `$a || $b`| *Or* (o inclusiu) | `true` si qualsevol de `$a` o `$b` és `true`.
| `$a xor $b` | *Xor* (o exclusiu) | `true` si `$a` o `$b` és `true`, pero no ambdós.
| `!$a` | *Not* (no) | `true` si `$a` no és `true`.

### Assignació

| Exemple | Nom | Resultat
| ---   | ---   | ---
| `$a = $b` | Assignació | Assigna a `$a` el valor de `$b`
| `$a += $b` | Assignació de la suma | Le suma a `$a` el valor de `$b`. Equivalent a `$a = $a + $b`
| `$a -= $b` | Assignació de la resta | Le resta a `$a` el valor de `$b`. Equivalent a `$a = $a - $b`
| `$a *= $b` | Assignació del producte | Assigna a `$a` el producto de `$a` por `$b`. Equivalent a `$a = $a * $b`
| `$a /= $b` | Assignació de la divisió | Assigna a `$a` el quocient de `$a` entre `$b`. Equivalent a `$a = $a / $b`
| `$a %= $b` | Assignació del residu | Assigna a `$a` el residu de dividir `$a` entre `$b`. Equivalent a `$a = $a % $b`
| `$a .= $b` | Concatenació | Concatena a `$a` la cadena `$b`. Equivalent a `$a = $a . $b`
| `$a++` | Increment | Incrementa `$a` en una unitat. Equivalent a `$a = $a + 1`
| `$a--` | Decrement | Decrementa `$a` en una unitat. Equivalent a `$a = $a - 1`

!!! Tip "Prioridad de los operadores"
    Recorda la prioritat. Primer els parèntesis, després la negació (`!`), productes/divisions, sumes/restes, comparacions, lògics i finalment es realitza l'assignació.
    Més informació a <https://www.php.net/manual/es/language.operators.precedence.php>

!!! question "Autoevaluación"
    Si `$a=5` i `$b=4`, esbrina el valor de `$c` si `$c = $a*2 > $b+5 && !($b<>4)`

#### Operador ternari

Funciona com un condicional **condició ? valor si true : valor si false** i que es pot simplificar ** condició	

<https://www.php.net/manual/es/language.operators.php>

Farem alguns **exercicis**: [Exercisi 2.0 Conceptes bàsics](2.0.Activitat.md)

## Estructures de control de flux
* Les instruccions de control de flux en PHP funcionen exactament igual que en altres llenguatges de programació.

* Les més habituals són:

  * Condicionals: if, if else, switch 
  * Bucles: while, do while, for

seguint les estructures:

```php
if (condició) {
	// instruccions
}
else {
	// instruccions
}
```
```php
switch ($variable) {
	case valor:
		//instruccio1
		break;
	case valor:
		//instruccio1
		break;
	default:
		//instruccio1
}			
```
```php
while (condició) {
	//instruccions
}
```
```php
do {
	//instruccions
} while (condició);
```
```php
for ($i=1;$i<10;$i++){
	//instruccions
}
```


<http://php.net/manual/es/language.control-structures.php>

### Sentències per a incloure Fitxers

Les sentències **include()** i **include_once()** i **require()** i **require_once()** inclouen i avaluen l'artxiu especificat. **include_once()** i **require_once()**  verifica que l'arxiu no haja sigut inclòs abans i és preferible a include. Cal ser curòs amb el path de l'arxiu a incloure. La diferència entre require i include és el tractament de l'error quan el fitxer no existeix.

```php
fruites.php
<?php

$color = 'verde';
$fruta = 'manzana';
include('fruite.view.php')

?>
```

```html
fruites.view.php

<html>
<head>
<title>Fruites</title>
</head>
<body>
	<h3>
 		<?= "Una $fruta $color" ?> 
 	</h3>		
</body>
</html>
```

#### Expansió de variables

* Podem introduir una variable dins d'un text sempre que usem les cometes dobles per a delimitar el text. Açò farà que el contingut de la variable s'expandisca i es concatene amb el text existent en la cadena.

```php
echo "<p>Mòdul: $module</p>"
```

* A voltes, és necessari envoltar-la entre claus

```php
echo "<p>Mòdul: {$module}DAW</p>"
```

* Si no posàrem les claus l'intèrpret cercaria una variable que es cride $moduleDAW

