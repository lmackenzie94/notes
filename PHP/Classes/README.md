# Classes

```php

<?php

// a class is a template used to create objects
class Person {

    // you must declare a visibility for any properties/methods inside of classes
    // these are PROPERTIES, not variables
    private $first = "Luke";
    private $last = "MacKenzie";
    private $age = "26";

    // this public method gives us access to the above private properties outside of this class
    public function owner() {
        // $this refers to the class
        // Note: since 'first' is a property (not variable), don't use $ to access it
        $a = $this->first;
        return $a;
    }
}

class Pet {
    // if this was 'private', we wouldn't be able to access it outside this class
    public function owner() {
        $a = "Hi there!";
        return $a;
    }
}

// INHERITANCE

class Person {
    // protected props are effectively private except for classes that extend this one
    protected $first = "Luke";
    private $last = "MacKenzie";
    private $age = "26";
}

// extending gives us access to any 'protected' props/methods of the Person class
// in this case, we can only access $first
class Pet extends Person {
    public function owner() {
        $a = $this->first;
        return $a;
    }
}

// To access owner method: 

$pet1 = new Pet();

// only works since 'owner' is public
echo $pet1->owner();

$person = new Person();
echo $person->owner(); // Luke

?>

<?php

// MORE ON PROPS & METHODS

class Person {

    // Properties (common to set as private and use a public method (ex: getName()) to provide access outside of this class)
    private $name;
    private $eyeColour;
    private $age;

    // CONSTRUCTOR
    // this will run at the beginning when you instantiate the class
    public function __construct($name, $age) {
        $this->name = $name;
        $this->age = $age;
    }

    // Methods

    // assigns value to the above properties
    public function setName($name) {
        $this->name = $name;
    }

    public function getName() {
        return $this->name;
    }
}

// index.php


$myself = new Person('Luke', 26); // the arguments passed here correspond to the ones in the construct() in our Person class
echo $myself->name; // Error
echo $myself->getName(); // 'Luke'

// we could then change the name later if we wanted
$myself->setName('Luca'); 


?>

```