# Ideas to show Understanding 
## Critique the use of find index instead of treating the object as a dict 
## Not Following the DRY Princible 
        - Critique the lack of use of dependancy injection for reducing the ammount of duplicated code ie : Passing a function as an argument to a function and allowing that function to execute in specific state 
        - the fact that all modules are just one big function
        - Having the same regex used in all uuid operation but not having it in it's own util function ie isUUID(id)
# : The Code is over 5 Years old and doesn't follow Current Programming paradigms 
    - Typescript / JSDOC



Write Part 6 

- running HTTP requests using an HTTP client: 
    -	demonstrate your understanding of Thunder client 
    -	demonstrate your understanding of the application’s behavior when a get request is submitted to the server with an invalid URL
    -	demonstrate your understanding of a get request that fetches a specific movie with a specific ID. This includes the use of regex, filter, substring, and split methods You are expected to run at least two cases of invalid requests.
    - demonstrate your understanding of a post request that creates a new movie that is written to the data file. This includes the use of bodyparser and write-to-file method. 
    - demonstrate your understanding of a delete request that deletes an existing movie. This includes the use of regex, filter, substring, index, findIndex and splice methods.
    - demonstrate your understanding of a put request that updates an existing movie. You are expected to explain the difference between the source code of delete and put request.


# Relation Between REST and CRUD 
RESTful APIs often use the HTTP protocol to implement CRUD operations here is a mapping of Crud operation to HTTP Methods 
Create (C) → POST: Used to create a new resource.
Read (R) → GET: Used to retrieve or fetch data from a resource.
Update (U) → PUT (or PATCH for partial updates): Used to modify an existing resource.
Delete (D) → DELETE: Used to remove a resource.


# Critique
a lot of the code violates the DRY principle as a lot of code is repeated between modules such as the regex for uuid validation so i think it should be refactored into it's own function here is one such example 
```js
const isValidUUID = (id) => {
  const regexV4 = new RegExp(
    /^[0-9A-F]{8}-[0-9A-F]{4}-4[0-9A-F]{3}-[89AB][0-9A-F]{3}-[0-9A-F]{12}$/i
  );
  return regexV4.test(id);
};
```
there is also:
- the json response sending 
- the Movie Data Query

the json is inefficiently written for the current use case since there are a lot of read and write operations accessed by id lookups so a more efficient approach would be a using the json as a key value store so it would be something like this 
```json
{
    "9017c8f4-3406-474a-a528-bac9da1675d8":
    {
        "title": "Avatar 2",
        "year": "2020",
        "genre": "Action, Adventure, Fantasy",
        "rating": "7.9",
    }
}
```

which would reduce the lookup from O(n) to O(1) here is a sample on how it would change 
```js

    if (!(id in req.movies)) {
      res.statusCode = 404;
      res.write(
        JSON.stringify({ title: "Not Found", message: "Movie not found" })
      );
      res.end();
    } else {
      // Delete the movie using delete operator
      delete req.movies[id];
      writeToFile(req.movies);
      res.writeHead(204, { "Content-Type": "application/json" });
      res.end(JSON.stringify(req.movies));
    }
```


# Assignment3
Blockchain technology is a decentralized and distributed ledger system that securely records and verifies transactions across multiple computers in a network.
you can Think of it as an immutable database. Here's a deeper explanation of each part of the definition:

Decentralization: Instead of relying on a central authority, the ledger is maintained by a network of nodes, ensuring transparency and reducing the risk of single-point failure.

Immutability: Once data is recorded on a blockchain, it is nearly impossible to alter, providing a high level of security and trust.

Transparency: All transactions are visible to participants in the network, enhancing accountability.