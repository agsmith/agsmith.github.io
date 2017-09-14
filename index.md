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

These objects will be available for CRUD operations via endpoints implemented in `htt4s` These endpoints will be serviced by a `ComicBookService` and `OrderService` with will interface with repositiory interpreter implemented with `doobie` to persist the domain objects


# [](#header-2) ... a bit about the tech stack
- http4s (http server)
- cats (functional library for scala)
- fs2 (stream library)
- doobie (jdbc interface for scala)


# [](#header-1) What's this all about

One of my goals for this fall is to more formally explore Scala and its surrounding eco system.  To this end I will create a Java Pet Store analog called Scala Comic Shop where I will develop an application using idomatic functional scala techniques and blog my notes and findings.
