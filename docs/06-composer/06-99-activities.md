# Activitats

## Projecte MovieFX 

### Introducció

601. La classe `FlashMessage`. 
     
     Fins ara, hem gestionat la comunicació entre pàgines mitjançant sessions. 
     La gestió la fèiem escrivint i llegint en les variables de sessió. L'objectiu de la següent classe és proporcionar-nos un mecanisme que ens facilite l'enviament de missatges entre pàgines. Una vegada implementada utilitza-la en la creació de pel·lícules.

```php
# src/Core/Helpers/FlashMessage.php
/**
 * Class FlashMessage
 * Aquesta classe llig i escriu directament en una variable de sessió 
 * que serà un array, la clau serà $sessionKey  de forma que evitem 
 * possible col·lisions.
*/
class FlashMessage
{
    /**
     * string
     */
    
    const SESSION_KEY = "flash-message";

    /**
     * obtenim el valor de l'array associat a la clau.
     * després de llegir-lo l'esborrem
     * si no existeix tornem el valor indicat per defecte.
     * @param string $key
     * @param mixed $defaultValue
     * @return mixed|string
     */
    public static function get(string $key, $defaultValue = '');

    /**
     * @param string $key
     * @param $value
     */
    public static function set(string $key, $value);

    /**
     * @param string $key
     */
    private static function unset(string $key);      
}
```

602.  Tenint en compte tot el procés de gestió de pujada de fixers, les restriccions que es poden aplicar, i les dades que ens interessen una vegada el procés s'ha efectuat exitosament, crea una classe que encapsule totes les funcionalitats requerides.

603. Implementa el patró `Registry` en una classe amb el mateix nom i afegeix una instancia de PDO associada a la 
clau "PDO". L'objecte PDO l'hauràs de crear i inserir-lo en el `Registre` en un nou fitxer anomenat `bootstrap.php`.

    Aquest fitxer serà requerit en totes els fitxers que tinguen accés a la base de dades.

604. En un fitxer de configuració (JSON, YAML, INI o XML, segons t'haja assignat el professor) emmagatzema el DSN (_Data Source Name_) d'accés a la base de dades. Després, crea una classe `Config` que llija el fitxer i extraga el DSN. Utilitza onfig` en `bootstrap.php` en lloc d'usar un literal en instanciar la classe PDO.

    Afig també al fitxer de configuració la ruta relativa on es guarden les fotos pujades.

605. Implementa els mètodes `Movie::toArray()`, `Movie::fromArray(Movie $obj)` i la classe `MovieMapper` tenint en compte la següent signatura:

```php
class MovieMapper
{
    private $pdo;

    public function __construct()
    {
        $this->pdo = Registry::getPDO();
    }

    public function find(int $id): ?Movie
    {
    }

    public function findAll(): array {
    }

    public function insert(Movie $obj)
    {
    }

    public function update(Movie $object)
    {
    }
}
```

606. Implementa el repositori de pel·licules tenint en compte la següent signatura:

```php
declare(strict_types=1);

class MovieRepository
{
    public MovieMapper $mapper;
    public function __construct()
    {
        $this->mapper = new MovieMapper();
    }

    public function save(Movie $movie) {

    }

    public function find(int $id):?Movie {
    }

    public function findAll():array {        
    }

    public function delete(Movie $movie) {

    }
}
```

### Composer

607.   En la següent activitat treballarem en Composer:

       1. Instal·la `composer` de forma global. 
       2. Instal·la `monolog`.
       3. Configura `bootstrap.php` perquè use l’autoloader de `Composer`.
       4. Configura `composer.json` perquè carregue les nostres classes.
       5. Configura `monolog` en `index.php` de forma que registre la activitat en `directori del projecte/app.log` i en Firefox amb l'extensió FirePHP.

608.   `webmozart/assert` és un paquet que conté una llibreria de funcions de validació (assercions/afirmacions).

    1. Instal·la el paquet.
    2. Configura'l si cal.
    3. Usa els seus mètodes per a validar els formularis.
    


