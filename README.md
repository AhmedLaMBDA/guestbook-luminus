# guestbook

## Architecture
├── Capstanfile
├── Dockerfile
├── Procfile
├── README.md
├── dev-config.edn
├── dev-resources
├── env
│   ├── dev
│   │   ├── clj
│   │   │   ├── guestbook
│   │   │   │   ├── dev_middleware.clj
│   │   │   │   └── env.clj
│   │   │   └── user.clj
│   │   └── resources
│   │       ├── config.edn
│   │       └── logback.xml
│   ├── prod
│   │   ├── clj
│   │   │   └── guestbook
│   │   │       └── env.clj
│   │   └── resources
│   │       ├── config.edn
│   │       └── logback.xml
│   └── test
│       └── resources
│           ├── config.edn
│           └── logback.xml
├── guestbook.iml
├── guestbook_dev.db.mv.db
├── guestbook_dev.db.trace.db
├── guestbook_test.db.mv.db
├── guestbook_test.db.trace.db
├── log
│   ├── guestbook.2024-01-04.0.log
│   ├── guestbook.2024-01-05.0.log
│   └── guestbook.log
├── project.clj
├── resources
│   ├── docs
│   │   └── docs.md
│   ├── html
│   │   ├── about.html
│   │   ├── base.html
│   │   ├── error.html
│   │   └── home.html
│   ├── migrations
│   │   ├── 20240104124910-guestbook.down.sql
│   │   └── 20240104124910-guestbook.up.sql
│   ├── public
│   │   ├── css
│   │   │   └── screen.css
│   │   ├── favicon.ico
│   │   ├── img
│   │   │   └── warning_clojure.png
│   │   └── js
│   └── sql
│       └── queries.sql
├── src
│   └── clj
│       └── guestbook
│           ├── config.clj
│           ├── core.clj
│           ├── db
│           │   └── core.clj
│           ├── handler.clj
│           ├── layout.clj
│           ├── middleware
│           │   └── formats.clj
│           ├── middleware.clj
│           ├── nrepl.clj
│           └── routes
│               └── home.clj
├── target
│   ├── base+system+user+provided+dev+test+test
│   │   ├── classes
│   │   │   └── META-INF
│   │   │       └── maven
│   │   │           └── guestbook
│   │   │               └── guestbook
│   │   │                   └── pom.properties
│   │   └── stale
│   │       └── leiningen.core.classpath.extract-native-dependencies
│   ├── classes
│   │   └── META-INF
│   │       └── maven
│   │           └── guestbook
│   │               └── guestbook
│   │                   └── pom.properties
│   ├── default
│   │   ├── classes
│   │   │   └── META-INF
│   │   │       └── maven
│   │   │           └── guestbook
│   │   │               └── guestbook
│   │   │                   └── pom.properties
│   │   └── stale
│   │       └── leiningen.core.classpath.extract-native-dependencies
│   ├── dev
│   │   ├── classes
│   │   │   └── META-INF
│   │   │       └── maven
│   │   │           └── guestbook
│   │   │               └── guestbook
│   │   │                   └── pom.properties
│   │   ├── repl-port
│   │   └── stale
│   │       └── leiningen.core.classpath.extract-native-dependencies
│   ├── repl-port
│   └── stale
│       └── leiningen.core.classpath.extract-native-dependencies
├── test
│   └── clj
│       └── guestbook
│           ├── db
│           │   └── core_test.clj
│           └── handler_test.clj
└── test-config.edn

### Core
The core manages the life cycle of the HTTP server

### Config
The config manages the map containing the configuration variables
used by the application

### Handler
The handler namespace is the root handler for the requests and
responses that aggregates all the routes

### Routes
The routes namespace contains the namespaces that are responsible
for handling different types of client requests

### DB
The db namespace is reserved for the data model of the application
and the persistence layer.

### Layout
The layout namespace contains common logic for generating the
application layout

### Middleware
The middleware namespace contains any custom middleware we
want to use in our application.

## Prerequisites

You will need [Leiningen][1] 2.0 or above installed.

[1]: https://github.com/technomancy/leiningen

## Running

To start a web server for the application, run:

    lein run 


## Graph the dependency tree
```clojure
(require '[mount.tools.graph :as graph])
=> nil
(graph/states-with-deps)
=>
({:name "#'guestbook.config/env", :order 1, :status #{:stopped}, :deps #{}}
 {:name "#'guestbook.db.core/*db*", :order 2, :status #{:stopped}, :deps #{"#'guestbook.config/env"}}
 {:name "#'guestbook.handler/init-app", :order 3, :status #{:stopped}, :deps #{}}
 {:name "#'guestbook.handler/app-routes", :order 4, :status #{:stopped}, :deps #{}}
 {:name "#'guestbook.core/http-server", :order 5, :status #{:stopped}, :deps #{"#'guestbook.config/env"}}
 {:name "#'guestbook.core/repl-server", :order 6, :status #{:stopped}, :deps #{"#'guestbook.config/env"}})

```

## License

Copyright © 2024 FIXME
