# fs2 (functional streams for scala)
I have worked with fs2 a bit over the past year, but this month I have begun to take the time to more fully understand the api.  When using working with fs2 streams, as with functional programming in general, it is desirable to push all side effects to the edge of the runtime universe.

# [](#header-1) Basic Architecture
In designing this sample application, it is my intent to use software best practices.  I will first set out to model my domain objects, `ComicBook` and `Order` 

```
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
