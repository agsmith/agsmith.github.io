# TLS Handshake

Below you will find a brief description of the TLS handshake process.  A TLS session always establishes that the Server is who it says it is. However, the Server can also request or require that the Client proves that it is who it says it is.  This can be configured as `CLIENT_AUTH: WANT` or `CLIENT_AUTH: NEED`.  This Client authentication process is referred to a Client Auth or Mutual Auth (since Server Auth is always implied).

## Server Authenticated TLS

### Client Hello: Client -> Server
- Client sends Server the highest TLS version it supports
- Client sends Server the cipher suites that it supports

### Server Hello: Client <- Server
- Server sends Client the agreed upon TLS version for the session
- Server sends Client the agreed upon cipher suite for the session
- Server sends Client its Certificate which contains its public key

### Client Key Exchange: Client -> Server
- Client validates that Servers certificate is signed by a trusted CA
- Client validates that the Server hostname matches that in the certificate
- Client extracts the Servers public key from the certificate
- Client generates a session key using the agreed upon cipher suite and TLS version parameters
- Client encrypts the session key in the Server's public key
- Client sends the Server the encrypted session key

### Client Finished: Client -> Server

### Server Finished: Client <- Server

### Encrypted Message Transfer: Client <-> Server

## Client of Mutually Authenticated TLS

### Client Hello: Client -> Server
- Client sends Server the highest TLS version it supports
- Client sends Server the cipher suites that it supports

### Server Hello: Client <- Server
- Server sends Client the agreed upon TLS version for the session
- Server sends Client the agreed upon cipher suite for the session
- Server sends Client its Certificate which contains its public key
- ** Server requests Client certificate (Client or Mutual Auth) **

### Client Key Exchange: Client -> Server
- Client validates that Servers certificate is signed by a trusted CA
- Client validates that the Server hostname matches that in the certificate
- Client extracts the Servers public key from the certificate
- Client generates a session key using the agreed upon cipher suite and TLS version parameters
- Client encrypts the session key in the Server's public key
- Client sends the Server the encrypted session key
- ** Client sends Server the clients certificate if it has been requested **

### ** Server Validates Client **
- ** Server validates the Clients certificate is signed by a trusted CA **
- ** Server validates the clients hostname matches that in the certificate **

### Client Finished: Client -> Server

### Server Finished: Client <- Server

### Encrypted Message Transfer: Client <-> Server


* * *

# fs2 (functional streams for scala)
I have worked with fs2 a bit over the past year, but this month I have begun to take the time to more fully understand the api.  When using working with fs2 streams, as with functional programming in general, it is desirable to push all side effects to the edge of the runtime universe.

# [](#header-1) Basic Architecture
In designing this sample application, it is my intent to use software best practices.  I will first set out to model my domain objects, `ComicBook` and `Order` 

```scala
case class ComicBook(
  title: Title,
  publisher: Publisher,
  authorName: AuthorName,
  isbn: ISBN,
  available: Boolean,
  price: Price)

case class Order(
  comic: ComicBook,
  orderDate: DateTime,
  shipDate: Option[DateTime] = None,
  status: OrderStatus = OrderStatus.Opened)
```

These objects will be available for CRUD operations via endpoints implemented in `http4s` These endpoints will be serviced by a `ComicBookService` and `OrderService` with will interface with repositiory interpreter implemented with `doobie` to persist the domain objects


# [](#header-2) ... a bit about the tech stack
- [http4s](http://http4s.org/) (http server)
- [cats](https://github.com/typelevel/cats) (functional library for scala)
- [fs2](https://github.com/functional-streams-for-scala/fs2) (stream library)
- [doobie](https://github.com/tpolecat/doobie) (jdbc interface for scala)


# [](#header-1) What's this all about

This project will create a Java Pet Store analog called Scala Comic Shop where I will develop an application using idomatic functional scala techniques and blog my notes and findings.
