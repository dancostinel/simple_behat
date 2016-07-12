Create a Doctrine Entity in YAML
================================
* # AppBundle/Entity/Person.php
```
<?php

namespace AppBundle\Entity;

class Person
{
    private $id;
    private $name;
    private $age;
}
```
* # AppBundle/Repository/PersonRepository.php
```
<?php

namespace AppBundle\Repository;

/**
 * PersonRepository
 *
 * This class was generated by the Doctrine ORM. Add your own custom
 * repository methods below.
 */
class PersonRepository extends \Doctrine\ORM\EntityRepository
{
}
```

* # AppBundle/Resources/config/doctrine/Person.orm.yml
```
AppBundle\Entity\Person:
    type: entity
    repositoryClass: AppBundle\Repository\PersonRepository
    table: persons
    id:
        id:
            type: integer
            generator:
                strategy: AUTO
    fields:
        name:
            type: string
            length: 20
            nullable: false
            column: Name
            unique: false
        age:
            type: integer
            nullable: false
            column: Age
            unique: false
```
* # php bin/console doctrine:schema:update --force