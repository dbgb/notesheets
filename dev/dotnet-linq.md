# Working with LINQ: Notesheet

- [Working with LINQ: Notesheet](#working-with-linq-notesheet)
  - [Operations](#operations)
    - [Restriction](#restriction)
    - [Projection](#projection)
    - [Partition](#partition)
    - [Sorting](#sorting)
    - [Grouping](#grouping)
    - [Sets](#sets)
    - [Conversion](#conversion)
    - [Retrieval](#retrieval)
    - [Generation](#generation)
    - [Quantifying](#quantifying)
    - [Aggregation](#aggregation)
    - [Sequences](#sequences)
    - [Joins](#joins)
  - [Eager vs. Lazy Execution](#eager-vs-lazy-execution)

## Operations

### Restriction

- The `where` clause of a LINQ query _restricts_ the output sequence.

- Only elements that match the given condition are added to the output sequence.

### Projection

- The `select` clause of a LINQ query _projects_ the output sequence.

- It is used to transform the input elements into the shape of the output
  sequence.

### Partition

- The methods `Take`, `Skip`, `TakeWhile` and `SkipWhile` _partition_ the output
  sequence.

- They are used to limit the portion of an input sequence transferred to the
  output sequence.

### Sorting

- The `orderby` clause of a LINQ query _sorts_ the output sequence.

- Sorting can be performed via single or multiple given criteria, and by
  `ascending` or `descending` order.

### Grouping

- The `group` \<element\> `by` \<property\> `into` \<group_name\> combination of
  keywords can be used to *group* an input sequence into buckets.

- Example \- Grouping a List of Words by First Letter:

```csharp
string[] words = { "blueberry", "chimpanzee", "abacus", "banana", "apple", "cheese" };

var wordGroups = from w in words
                 group w by w[0] into g
                 select (FirstLetter: g.Key, Words: g);

foreach (var g in wordGroups)
{
    Console.WriteLine("Words that start with the letter '{0}':", g.FirstLetter);
    foreach (var w in g.Words) Console.WriteLine(w);
    Console.Write("\n");
}
```

### Sets

- The methods `Distinct`, `Union`, `Intersect`, and `Except` provide operations
  for comparing multiple _sets_ of data.

### Conversion

- The methods `ToArray`, `ToList`, `ToDictionary`, and `OfType` provide ways to
  _convert_ LINQ results to collections.

### Retrieval

- The methods `First`, `FirstOrDefault`, `Last`, `LastOrDefault`, and
  `ElementAt` _retrieve_ elements based on the position of that element in the
  sequence.

### Generation

- The methods `Range` and `Repeat` _generate_ sequences of integers.

- Generated sequences can be used as the source for LINQ queries.

### Quantifying

- The _quantifier_ methods `Any` and `All` determine whether elements match a
  given condition.

### Aggregation

- Aggregator methods return a _single value_ calculated _from all_ the elements
  in a sequence.

- These methods include `Count`, `Sum`, `Min`, `Max`, `Average`, and
  `Aggregate`.

### Sequences

- Sequence methods operate compare or manipulate _entire sequences_, rather than
  the individual elements of a sequence.

- These methods include `SequenceEqual`, `Concat`, and `Combine`.

### Joins

- Join clauses perform in a similar fashion to SQL join operators, allowing data
  from _one collection to be used to select the data in a different collection_.

- Cross joins, group joins, and left outer joins can all be performed in LINQ
  queries, using the `join`, `in`, `on`, `into` and `equals` keywords.

## Eager vs. Lazy Execution

- By default, queries are executed _lazily_ \- meaning that query execution is
deferred until it is evaluated i.e. at the point it is enumerated over.

- This means that queries can be used again after data changes \- and will then
  operate on the updated data.

- Example \- Lazy Execution:

```csharp
int[] numbers = { 5, 4, 1, 3, 9, 8, 6, 7, 2, 0 };

var lowNumbers = from n in numbers
                 where n <= 3
                 select n;

Console.WriteLine("First run numbers <= 3:");
foreach (int n in lowNumbers) Console.WriteLine(n);

// Inverting each number in the source array
for (int i = 0; i < 10; i++) numbers[i] = -numbers[i];

// Due to lazy execution, on the second run, the same LINQ query object is able
// iterate over the updated source array, producing different results from the
// first run
Console.WriteLine("Second run numbers <= 3:");
foreach (int n in lowNumbers) Console.WriteLine(n);
```

- If _eager_ execution is desired, conversion methods such as `ToList` or
  `ToArray` can be used to force immediate query execution.
