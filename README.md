# N-Meta Ⓜ️
[![Swift Version](https://img.shields.io/badge/Swift-5.2-brightgreen.svg)](http://swift.org)
[![Vapor Version](https://img.shields.io/badge/Vapor-4-30B6FC.svg)](http://vapor.codes)
[![Circle CI](https://circleci.com/gh/nodes-vapor/n-meta/tree/master.svg?style=shield)](https://circleci.com/gh/nodes-vapor/n-meta)
[![codebeat badge](https://codebeat.co/badges/5dfa4439-cd97-4210-8595-40b57830196a)](https://codebeat.co/projects/github-com-nodes-vapor-n-meta-master)
[![codecov](https://codecov.io/gh/nodes-vapor/n-meta/branch/master/graph/badge.svg)](https://codecov.io/gh/nodes-vapor/n-meta)
[![Readme Score](http://readme-score-api.herokuapp.com/score.svg?url=https://github.com/nodes-vapor/n-meta)](http://clayallsopp.github.io/readme-score?url=https://github.com/nodes-vapor/n-meta)
[![GitHub license](https://img.shields.io/badge/license-MIT-blue.svg)](https://raw.githubusercontent.com/nodes-vapor/n-meta/master/LICENSE)


This package enforces clients to send a specific header in all requests:

```
N-Meta: [PLATFORM];[ENVIRONMENT];[APP_VERSION];[DEVICE_OS];[DEVICE]
```

If you're running an older version of Vapor then have a look here:

- [Vapor 1.x](https://github.com/nodes-vapor/n-meta/tree/vapor-1)
- [Vapor 2.x](https://github.com/nodes-vapor/n-meta/tree/vapor-2)
- [Vapor 3.x](https://github.com/nodes-vapor/n-meta/tree/vapor-3)

This header can look like this `android;production;1.2.3;4.4;Samsung S7`
 - platform
 - environment
 - app version
 - device os
 - device

For web platform only platform and environment is required, since the rest can be found in `User-Agent`.

Why not just use `User-Agent`?
 - `User-Agent` is missing some of these details
 - `User-Agent` can be hard to extend/override
 - Default `User-Agent` in iOS & Android can be their client (OkHttp, Alamofire etc).


## 📦 Installation

Update your `Package.swift` file.
```swift
    ...
    dependencies: [
        ...
        .package(url: "https://github.com/nodes-vapor/n-meta.git", from: "4.0.0")
    ],
    targets: [
        .target(
            name: "App",
            dependencies: [
                ...
                .product(name: "NMeta", package: "n-meta"),
            ]
        )
        ...
```

## Getting started 🚀

Configure NMeta as per your needs, for example: 

```swift
app.nMeta = .init(exceptPath: ["/admin"])
```

Next, add the middleware directly to your routes (e.g. in `routes.swift`):

```swift
app.grouped(NMetaMiddleware()).get("hello") { req in
    "Hello, world!"
}
```

or add the middleware globally (e.g. in `configure.swift`) which will add it to all routes:

```swift
app.middlewares.use(NMetaMiddleware())
```

## 🏆 Credits

This package is developed and maintained by the Vapor team at [Nodes](https://www.nodesagency.com).


## 📄 License

This package is open-sourced software licensed under the [MIT license](http://opensource.org/licenses/MIT)
