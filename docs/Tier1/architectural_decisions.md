# Architectural Decisions

### Processing first, then outputting the result

When we are processing a large data-set we need to be careful with the performace of our operations because we could end up reaching our maximum memory allowed to use value. For example if we are trying to save information into the database, and we are using a loop to iterate over an array structure,there is a really importance difference if we call the **INSERT** operation inside or outside the loop.

```php
<?php

$vehicleQuery = $db->query('SELECT * FROM vehicle');
$vehicleList = $vehicleQuery->fetch(PDO::FETCH_ASSOC);

// Moving vehicle list to a history table
foreach ($vehicleList as $vehicle) {
    $saveVehicleHistory = $db->prepare("INSERT INTO vehicle_history VALUES (:id, :model)");
    $saveVehicleHistory->bindValue(':id', 1, PDO::PARAM_INT);
    $saveVehicleHistory->bindValue(':model', 'Toyota', PDO::PARAM_STR);
    $saveVehicleHistory->execute();
}
```

With the previous code, each time that the loop iterate over a vehicle row, it will execute a call with an **INSERT** operation, causing a lack of memory issue if we are trying to move a bunch of vehicles into our history table.

We can solve that problem, by processing first the vehicles list to insert and call the **INSERT** operation just once.

```php
<?php

$vehicleQuery = $db->query('SELECT * FROM vehicle');
$vehicleList = $vehicleQuery->fetch(PDO::FETCH_ASSOC);

$vehiclesHistoryArray = [];

// Moving vehicle list to a history table
foreach ($vehicleList as $vehicle) {
   $vehiclesHistoryArray[] = ['id' => $vehicle->id, 'model'=> $vehicle->model];
}

// ... We can convert the array to a string like:
// $vehicleValuesString = '(1, Toyota), (2, GMC), (3, Chevrolet)'

$saveVehicleHistory = $db->prepare("INSERT INTO vehicle_history VALUES :values");
    $saveVehicleHistory->bindValue(':values', $vehicleValuesString, PDO::PARAM_STRING);
    $saveVehicleHistory->execute();
```

### Using an ORM

### Pros of using an ORM

- It's completely agnostic from the database engine that you want to use, you can easily change between MySQL and PostgreSQL if you want to.
- It allows you to write queries in an object oriented way, and translates that into the proper SQL query.
- It abstracts away the database system so that switching from MySQL to PostgreSQL, or whatever flavor you prefer, is easy-peasy.
- Depending on the ORM you get a lot of advanced features out of the box, such as support for transactions, connection pooling, migrations, seeds, streams, and all sorts of other goodies.
- Many of the queries you write will perform better than if you wrote them yourself.

### Best PHP ORMs

- Eloquent
- Doctrine

### Query Example using an ORM

```php
$query = $em->createQueryBuilder();
$query->select('v')
  ->from(Vehicle::class, 'v')
  ->leftJoin('v.owner', 'owner')
  ->where('owner.name = :name')
  ->setParameter('name', 'Roberto');

$result = $query->getQuery()->getResult(); // array by default  
```

### Eloquent vs Doctrine

When talking about these two ORM an important topic to take into consideration are the design patterns that are behind them. Eloquent implements Active Record whereas Doctrine is based on DataMapper + Repository. I think Active Record is a very good design pattern when you are working on a small application where you business logic is not complex at all. Since it forces your model to be tied to the ORM when extending from a base Model class. The ability to use the same class to execute operations over itself could appear an easy way to go, but it's not following the Single Responsability Principle from SOLID. In the other hand, Doctrine allows you to delegate those operations to a specific class, then your model will be just a plain PHP object not tied to any other class/component.

### Documentation

- [Eloquent Documentation](https://laravel.com/docs/5.8/eloquent#introduction)

- [Doctrine Documentation](https://www.doctrine-project.org/)

- [Comparison between Eloquent and Doctrine](https://culttt.com/2014/07/07/doctrine-2-different-eloquent/)