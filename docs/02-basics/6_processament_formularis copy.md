# 6. Processament de formularis

## Introducció

### Què és una petició HTTP?

Una petició HTTP és una sol·licitud d'un recurs a un servidor. La petició es realitza a través d'una URL. Amb la petició s'envien també paràmetres.

Hi ha diferents mètodes (METHOD) per a realitzar una petició (GET, POST, PUT, DELETE, PATCH, etc.). Els més habituals són GET i POST. La resta són més utilitzats en les RESTful API.

![Sol·licitud HTTP](assets/http-request.png)


## Mètodes GET i POST

### Mètode GET

S'utilitza per a sol·licitar dades d'un recurs. Mostren els paràmetres que 
s'envien en la url. Es poden utilitzar directament en enllaços. 
El resultat es pot emmagatzemar en cache. Romanen en l'historial del navegador. 
La grandària dels paràmetres està limitat a 255 caràcters.

*Exemple de petició GET*
![Petició GET](assets/get-example.png)

*Inspecció de la petició*
![Inspecció del petició GET: Capçaleres](assets/get-inspect-headers.png)

*Inspecció de la petició*
![Inspecció del petició GET: Paràmeters](assets/get-inspect-parameters.png)


#### Accedir a les dades de la petició GET

Per a accedir a les dades usem la variable superglobal `$_GET`.
    
`$_GET` és un array associatiu les claus del qual coincidiran amb els noms que li hem donat als paràmetres.

Per a accedir als paràmetres de la petició anterior:

```php
echo $_GET['nom'].' '.$_GET['cognom']; // Homer Simpson
```

### Mètode POST

El mètode POST té les següents característiques:

* S'utilitza per a enviar dades a un recurs.
* Els paràmetres van en el cos de la petició, no són visibles per a l'usuari.
* La petició no es guarda en cache.
* No es pot utilitzar en un enllaç.
* No roman en l'historial.
* No tenim la limitació de grandària dels paràmetres.
* Es solen utilitzar en els formularis.

##### Evitar el CSRF

En tota pàgina que reba paràmetres GET has de comprovar el **HTTP referer** del navegador, i que aquest siga de dins de la teua web. En php el referer que envia el navegador s'emmagatzema en `$_SERVER['HTTP_REFERER']`.

Seria tal com:

 ```php
 if(parse_url($_SERVER['HTTP_REFERER'], PHP_URL_HOST)!=$_SERVER['HTTP_HOST']) 
    die('Anti-CSRF'); 
 ```

!!! important
    Amb aquest codi estem obligant al fet que el navegador envie un _referer_ si o sí. Per tant només ha d'utilitzar-se en pàgines a les quals el navegador accedisca des d'una altra pàgina de la nostra web.

    Òbviament no podem col·locar-ho en la primera pàgina a la qual s'accedeix a la nostra web (`index.php` o similar), ja que si l'usuari a escrit l'adreça a mà en la barra del navegador no s'enviarà referer cap i saltarà el sistema.


## Definició de formularis 

Com hem dit abans el mètode POST s'empra en els formularis. El formulari següent enviarà les dades a la pàgina `index.php` (atribut `action` de l'element `form`).

Utilitza el mètode `post` indicat en l'atribut `method`:

```html
<form action="index.php" method="post">
    <label for="nom">Nom</label>
    <input type="text" name="nom" value="">
    <br />
    <label for="cognom">Cognom</label>
    <input type="text" name="cognom" value="">
    <br />
    <input type="submit" value="Enviar">
</form>
```

*Inspecció de la petició: Headers*
![Inspecció del petició POST](assets/post-inspect-headers.png)

*Inspecció de la petició: Paramètres*
![Inspecció del petició POST](assets/post-inspect-parameters.png)


### Accedir a les dades de la petició POST

Usem la variable superglobal `$_POST`. Funciona igual que `$_GET`, però amb els noms (atribut `name`) que li hem donat als camps del formulari.

En depuració podem mostar totes les dades rebudes:
        
```php
var_dump ($_POST);
print_r($_POST)
```

Per a mostrar les dades individualment:

```php
echo $_POST['nom'];
echo $_POST['cognom'];
```


### Accedir a paràmetres no existents

Errors del tipus  

```
Notice: Undefined index: nom in /home/ubuntu/index.php on line 6
```
ens indiquen que la clau `nom`  no existeix en l'array `$_POST`. La variable supergloblal `$_POST` està buida si no s'ha
enviat el formulari.

Per a evitar aquest tipus d'errors és important verificar que s'haja enviat el formulari prèviament:

```php
if ($_SERVER['REQUEST_METHOD'] === 'POST')
{

}
```

## Validació de formularis 

Hem de comprovar que les dades que envia el formulari són correctes.

Les validacions a realitzar són les següents:

1. Els camps requerits no han de quedar buits. Ni contenir espais en blanc a l'inici i al final.
2. Els camps email i data han de tenir el format esperat.
3. Tots els camps s'han de filtrar amb `htmlspecialchars` per a evitar atacs de _Cross-site Scripting_ (XSS).

### Valors buits

1. Els camps requerits no deurien quedar-se buits.
2. Per a verificar que un valor no queda buit podem utilitzar la funció `empty()` de PHP.

### Espais en blanc

1. Hem d'eliminar els espais en blanc del principi i final dels camps.
2. S'utilitza la funció `trim`

### Escapar l'entrada

Sempre hem de filtrar l'entrada amb `htmlspecialchars` abans de mostrar el camp amb `echo` o similar. Acò convertirà
qualsevol caràcter especial d'html en la entitat, així no interferirà en el el programa.

### Comprovar l'email

Per a verificar si un email és correcte podem utilitzar la funció `filter_var` 

```php
filter_var($email, FILTER_VALIDATE_EMAIL)
```
o la funció `filter_input` quan obtenin les dades directament d'una variable extern.

```php
// suposem que rebem les dades d'un formulari que té un quadre de text de nom 'email'
$email = filter_input(INPUT_POST, 'email', FILTER_VALIDATE_EMAIL)

```

#### filter_input

```php
filter_input(int $type, string $variable_name[, int $filter=FILTER_DEFAULT[, mixed $options]]):mixed
```
La funció `filter_input` agafa una variable externa (`$_GET`, `$_POST`, etc) concreta pel seu nom i aplica el filtre indicat.

Els filtres poden [sanejar](https://www.php.net/manual/es/filter.filters.validate.php) o [validar](https://www.php.net/manual/es/filter.filters.sanitize.php) les variables externes.

Per exemple, si volem agafar el valor del paràmetre *nom*  del querystring (http://localhost/index.php?nom=<h1>Homer</h1>) usarem el tipus INPUT_GET.

El fltre FILTER_SANITIZE_STRING elimina etiquetes, i opcionalment elimina o codifica caracters especials.

```php
$nom = filter_input(INPUT_GET, 'nom', FILTER_SANITIZE_STRING).  // $nom = Homer
```

Més informació en:

* [filter_var](http://php.net/manual/es/function.filter-var.php)
* [filter_input](http://php.net/manual/es/function.filter-input.php)

### Comprovar la data

* Per a comprovar la data hem de crear una funció a aquest efecte.
* Podem utilitzar el mètode estàtic `createFromFormat` de la classe `DateTime`

Més informació: [http://php.net/manual/es/datetime.createfromformat.php](http://php.net/manual/es/datetime.createfromformat.php)

#### Exemple

```php
$data1 = "2001-05-02"; // Data és de tipus string
// DateTime::createFromFormat converteix una cadena de text a on objecte DateTime
// ens tornarà una instància de DateTime o FALSE en cas d'error.

$dt1 = DateTime::createFromFormat('Y-m-d', $data1);  

if ($dt1 === false) {
    echo "La data d'inici és incorrecta";
}
```

https://www.php.net/manual/es/function.strtotime.php

També és habitual trobar els controls de data separats en 3 elements input. Un per a l’any, l’altre per a mes i l’altre per al dia.



## Bones pràctiques en l’obtenció de dades des de l’exterior

Cal seguir les següents bones pràctiques:

1. No confieu mai (mai) en l’entrada des de l’exterior del vostre PHP.
2. Sanegeu i valideu l’entrada de dades sempre.
3. Les funcions `filter_var()` i `filter_input()` poden sanejar el text i validar els formats de text (per exemple, adreces de correu electrònic, enters).
4. Recordeu que l’entrada de dades no es limita a formularis enviats per l’usuari. Els fitxers carregats i descarregats, els valors de sessió, les dades de galetes i les dades de serveis web de tercers també són d’entrada estrangera.

A mode de resum podíem resumir la gestió de formularis en el següent diagrama de flux.

![Form handle](images/form-handle.png)

### Formularis en HTML5  

En els següents recursos trobaràs informació addicional sobre els controls de formularis en HTML5:
* [Formularios en HTML](https://developer.mozilla.org/es/docs/Learn/HTML/Forms) en MDN web docs.
* [Formularios en HTML5](https://developer.mozilla.org/es/docs/HTML/HTML5/Forms_in_HTML5) en MDN web docs.
* [HTML Forms](https://www.w3schools.com/html/html_forms.asp) en W3CSchools.

## Activities

### Activit 261

Crea una pàgina que reba com a paràmetre un nom i mostre el text ‘Benvingut [nom]!!!’ sent [nom] el nom has 
passat com a paràmetre.

Guarda-la amb el nom `exemple_get.php`.

### Activitat 12 A: Creació d'un formulari

Crea un formulari que tinga els següents camps:
        
* Nom i cognoms
* Data de naixement
* Correu electrònic
* Assumpte
* Missatge

En l'atribut `action` del formulari posarem el següent:

```php
action="<?= $_SERVER['PHP_SELF']; ?>"
```

Açò farà que siga la pròpia pàgina del formulari la que processe les dades del mateix.

En prémer `Enviar` han d'aparèixer sota el formulari les dades que s'han introduït en el mateix.

### Activitat 12 B: Creació d'un formulari

Soluciona el problema dels paràmetres no enviats de l'exercici anterior.

### Activitat 12 C: Validació d'un formulari

Modifica l'exercici anterior realitzant les validacions oportunes.
