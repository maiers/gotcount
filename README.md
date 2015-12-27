# gotcount
A column based in-memory database with a url compatible query language and very small response times

# how to use

- Run it with `gotcount-service.jar server config.yml`
- Open `localhost:8080` to access the service. The server will return path options if available

# Query Language

Append `?query=` to any data returning url to define a filter. `attribute=1` will filter on the column attribute with the value 1. Add more attribute filters by using the semicolon devider `;`.

    Query := Filter(';' Filter)*
    Filter := column ':' Action 
    Action := Value | UnaryOperation | BinaryOperation | SetOperation
    UnaryOperation := ( '!' | '>' | '<' ) Value
    BinaryOperation := Value '-' Value
    SetOperation := ( 'IN' | '!IN' ) ( Value | ( '[' | '(' ) Value (',' Value)* ( ')' | ']' ) )
    Value := Number | String

## Structure

gotcount is split into four projects:

- *-core: the database itself
- *-parser: the query parser
- *-query: the query atoms
- *-service: the web/rest service

## Libraries

gotcount makes heavy use [Compressed Bitmaps](https://github.com/lemire/javaewah) on the data layer and uses [parboiled](https://github.com/sirthias/parboiled/wiki) for query parsing. The service component is build using [Dropwizard](http://www.dropwizard.io/).
