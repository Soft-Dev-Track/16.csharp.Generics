# 16.Generics

Generics, a key feature introduced with .NET 3.5 and C# 2, have been around for quite some time. They offer a robust way to create classes, methods, and interfaces where the data type is specified later.

This capability is crucial in several contemporary programming languages and plays a vital role in enabling LINQ (Language Integrated Query)—a powerful querying technology integrated directly into the language. Curious about LINQ? Patience, young grasshopper, your exploration of this topic is just on the horizon.

(Generics also serve as a prime example of polymorphism, a fundamental concept in object-oriented programming!)

## 1. Basics of Generic Types
Generic types allow you to write a class or method that can work with any data type. This is done by specifying a placeholder (typically called T) for the data type when defining the class or method. 

Later, when you use this class or method, you can specify the actual data type you want to use with it. This approach helps in creating flexible, reusable code.

```csharp 
using System;
using System.Collections.Generic;

public class SimpleList<T> 
{
    private List<T> _items = new List<T>();

    public void Add(T item)
    {
        _items.Add(item);
    }

    public T Get(int index)
    {
        if (index < 0 || index >= _items.Count)
        {
            throw new IndexOutOfRangeException("Index out of range");
        }
        return _items[index];
    }
}
```

### Explanation
- **Generic Class Definition**: The `SimpleList<T>` class is defined with a type parameter `T`, which means it can store items of any type determined at runtime. The `_items` field is a list that holds items of type `T`.

- **Methods**:
    - **Add Method**: This method accepts an item of type `T` and adds it to the _items list.
    - **Get Method**: This method retrieves an item by its index from the `_items` list. It throws an exception if the index is out of bounds.


## 2. Type Constraints in Generics
Type constraints in C# generics specify the requirements for type arguments in generic classes or methods. These constraints ensure that a type implements an interface, derives from a class, or has a public constructor, enhancing code safety and flexibility.

### 3. Key Concepts
- **Definition**: Use the `where` keyword in a generic definition to apply constraints.
- **Common Constraints**:
    - `where T : struct` — T must be a value type.
    - `where T : class` — T must be a reference type.
    - `where T : new()` — T must have a public parameterless constructor.
    - `where T : InterfaceName` — T must implement the specified interface.
    - `where T : ClassName` — T must derive from the specified class.

Consider a generic `Repository<T>` where `T` must implement an `IIdentifiable` interface with an `ID` property. This constraint allows the repository to manage diverse entities by their ID in a type-safe way.

```csharp 
public interface IRepository<T> where T : class
{
    IEnumerable<T> GetAll();
    T GetById(int id);
    void Add(T entity);
    void Update(T entity);
    void Delete(T entity);
}

public class Repository<T> : IRepository<T> where T : class
{
    private readonly List<T> _entities = new List<T>();

    public IEnumerable<T> GetAll()
    {
        return _entities;
    }

    public T GetById(int id)
    {
        // Simulate fetching entity by ID
        return _entities[id];
    }

    public void Add(T entity)
    {
        _entities.Add(entity);
    }

    public void Update(T entity)
    {
        // Logic for updating entity
    }

    public void Delete(T entity)
    {
        _entities.Remove(entity);
    }
}
``` 

**Interface: IRepository<T>**

The `IRepository<T>` interface is defined with a type constraint `where T : class`, which means it can only be implemented for reference types (classes). This interface declares five methods:
- **GetAll()**: Returns an IEnumerable<T> representing all entities in the repository. IEnumerable<T> is a collection that can be iterated over, typical in read operations.
- **GetById(int id)**: Retrieves a single entity by its identifier. It returns an object of type T.
- **Add(T entity)**: Adds a new entity to the repository.
- **Update(T entity)**: Updates an existing entity in the repository. The actual logic for updating would depend on how entities are tracked for changes.
- **Delete(T entity)**: Removes an entity from the repository.

**Implementation: Repository<T>**
The `Repository<T>` class implements the `IRepository<T>` interface, again constrained to operate on reference types. It manages a list of entities using a private field _entities.

- **GetAll()**: Simply returns the list of all entities.
- **GetById(int id)**: Simulates fetching an entity by its index in the list. Note, in a real-world scenario, you would typically use a more complex method of identifying and retrieving entities, such as searching by a unique identifier.
- **Add(T entity)**: Adds the entity to the list. This operation is straightforward as it just appends the entity to the collection.
- **Update(T entity)**: This method would contain logic to find an existing entity in the collection and update its values. In this code snippet, the method is empty because updating logic can vary significantly depending on the context, such as tracking changes and applying them to a database.
- **Delete(T entity)**: Removes the entity from the list. This is direct and affects the collection immediately.

## 4. Exercices

---

![](https://media1.giphy.com/media/v1.Y2lkPTc5MGI3NjExcGJsMzVwNWFtMmVjemRudHNyZHAxcTgyM2Z1bHBwdm95bzNzZ2RzNyZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/Q1aRmd8e90WIw/giphy.gif)