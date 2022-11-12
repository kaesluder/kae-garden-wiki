# Working Figwheel Setup

#### Running

```shell
clojure -m figwheel.main --build dev --repl
# or 
clojure -M:fig -b dev -r
```

#### `deps.edn`

```clojure
{:deps {org.clojure/clojure {:mvn/version "1.9.0"}
        org.clojure/clojurescript {:mvn/version "1.10.773"}
        com.bhauman/figwheel-main {:mvn/version "0.2.18"}
        ;; optional but recommended		
        com.bhauman/rebel-readline-cljs {:mvn/version "0.1.4"}}
 :aliases {:fig {:main-opts ["-m" "figwheel.main"]}}}
```

#### `dev.cljs.edn`

Defines the `main` function for a build. 

```clojure
^{:extra-main-files {:testing {:main example.test-runner}}}
{:main example.core}
```

#### `figwheel.edn`

```clojure
{:watch-dirs ["src" "test"]
 :css-dirs ["resources/public/css"]
 :auto-testing true}
```

#### test runner

```clojure
;; This test runner is intended to be run from the command line
(ns intentional-startpage.test-runner
  (:require
   [cljs-test-display.core]
   [cljs.test :refer-macros [run-tests]]
    ;; require all the namespaces that have tests in them
   [intentional-startpage.core-test]
   [intentional-startpage.weather-test]))

(run-tests (cljs-test-display.core/init! "app")
           'intentional-startpage.core-test
           'intentional-startpage.weather-test)

```

Auto testing URL: http://localhost:9500/figwheel-extra-main/auto-testing


Source: [figwheel docs: Testing](https://figwheel.org/docs/testing.html) .   
Source: [figwheel docs: Installation](https://figwheel.org/docs/installation.html)