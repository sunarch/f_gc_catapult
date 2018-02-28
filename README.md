# Catapult

***Catapult*** is a web framwork for ***Igropyr***

with it

easily to write the router

```
(define router
    (get
        ("/"        index)
        ("/index"   index)
        ("/users"   users)
        ("/notes"   notes)))
```

easily to define respone

```
(define index
    (lambda (req)
        (res
            ('content   "Hello world"))))

(define index
    (lambda (req)
        (res
            ('status    200)
            ('type      "text/html")
            ('content   req))))
```

a classic style, the elements may define by free order.

```
(define index
    (lambda (req)
        (res "hello world")))

(define index
    (lambda (req)
        (res 200 "hello world")))

(define index
    (lambda (req)
        (res "text/html" "<h1>hello world</h1>")))
        
(define index
    (lambda (req)
        (res 200 "text/html" "<h1>hello world</h1>")))
```

a short style

(res string)                => respone content only

(res int string)            => respone status and content

(res string string)         => respone style and content

(res int string string)     => respone status, style and content

in this style the ordre is very important!


and use

```
(define request
    (callback
        (lambda (request_header pathinfo query_string)
            ((ref router pathinfo) query_string))))
```

instead of

```
(define request
    (callback
        (lambda (request_header pathinfo query_string)
                    (respone "200 OK" "text/html" 
                        (string-append "<p>path is:" pathinfo "</br>query is:" (if query_string query_string "nothing"))))))
```
