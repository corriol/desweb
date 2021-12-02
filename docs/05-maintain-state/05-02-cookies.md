# Galletes (*cookies*)

Una galleta és un fitxer de text que un lloc web guarda a l'entorn de l'usuari de navegador. El seu ús més típic és
l'emmagatzematge de les preferències de l'usuari (per exemple, l'idioma en que s'han de mostrar les pàgines), perquè no
hagi de tornar a indicar-les la propera vegada que visiteu el lloc.

Si utilitzes Firefox com a navegador, pots accedir a `Desenvolupador web` &ndash; `Inspector d'emmagatzematge` des del
menú principal. Entre les seves característiques et permet consultar i editar les galetes emmagatzemades en el mateix.

![Inspeccionar galetes en Firefox](images/galetes-firefox.png)

En PHP, per emmagatzemar una galleta al navegador de l'usuari, pots utilitzar la funció `setcookie`. L'únic paràmetre
obligatori que has de fer servir és el nom de la galleta, però admet diversos paràmetres més opcionals.

```php
 setcookie(
    string $name,
    string $value = "",
    int $expires = 0,
    string $path = "",
    string $domain = "",
    bool $secure = false,
    bool $httponly = false
): bool
```

!!! info 
    Per a més informació consulta: [https://www.php.net/manual/es/function.setcookie.php](https://www.php.net/manual/es/function.setcookie.php).


Per exemple, si vols emmagatzemar en una galleta la data del darrer accés d'un usuari, pots fer:

```php
setcookie ("last_visit_date", (string) time(), time() + 3600);
```

Els dos primers paràmetres són el nom de la galleta i el seu valor. El tercer és la data de caducitat de la mateixa en format `timestamp` (en l'exemple, un hora des del moment en què s'execute). En cas de no figurar aquest paràmetre, la galleta s'eliminarà quan es tanque el navegador. Tingues en compte que també es poden aplicar restriccions a les pàgines del lloc que poden accedir a una galleta en funció de la ruta.

Les galetes es transmeten entre el navegador i el servidor web utilitzant les capçaleres del protocol 
HTTP. **Per això, les sentències `setcookie` s'han d'enviar abans que el navegador mostre cap informació a pantalla.**

![Enviament de cookies HTTP](assets/cookie-http-transfer.png)

Podeu trobar més informació en [Ultimate Guide to HTTP Cookies](https://blog.webf.zone/ultimate-guide-to-http-cookies-2aa3e083dbae)

El procés de recuperació de la informació que emmagatzema una galleta és molt simple. Quan accedeixes a un lloc web, el
navegador li envia de forma automàtica tot el contingut de les galetes que emmagatzema relatives a aquest lloc en
concret. Des PHP pots accedir a aquesta informació per mitjà de l'array `$_COOKIE`.

!!! warning 
    Sempre que utilitzeu galetes en una aplicació web, heu de tenir en compte que en última instància la seva 
    disponibilitat està controlada pel client. Per exemple, alguns usuaris deshabiliten les galetes al navegador perquè 
    pensen que la informació que emmagatzemen pot suposar un potencial problema de seguretat. O que la informació que
    emmagatzemen pot arribar a perdre perquè el usuari decideix formatar l'equip o simplement eliminar-les de sistema.


Si un cop emmagatzemada una galleta al navegador vols eliminar-la abans que expire, pots utilitzar 
la mateixa funció `setcookie` però indicant una data de caducitat anterior a l'actual.

!!! question
    Quina és la durada per defecte d'una galleta si no s'indica la data de caducitat, com en la següent crida a la funció `setcookie`?

    ```php
    setcookie ("idioma", "espanyol");
    ```

    1. Fins que es tanque el navegador de l'usuari.
    2. 1 hora.

## Problemes de seguretat relacionats amb galletes

A l'hora de fer ús de galletes, cal ser conscient dels potencials problemes de seguretat que 
poden patir.

En l'article [Ultimate Guide to HTTP Cookies](https://blog.webf.zone/ultimate-guide-to-http-cookies-2aa3e083dbae) s'exposen tres dels problemes més rellevants i la seua sol·lució.

Aquest article és una referència molt completa dels possibles valors i atributs que es poden fer servir les galletes: [Set-Cookie headers](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Set-Cookie)