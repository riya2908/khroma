# Khroma

Khroma is a ClojureScript library which provides access to Chrome Extension API. It wraps API with idiomatic functions 
and heavily uses core.async for asynchronous API interaction.

Khroma is still a work in progress, so not all APIs are implemented and well tested. The long term goal is to cover all Chrome 
and Chrome OS API's to make use of ClojureScript for extensions and applications development as convenient as possible.

## Installation

Add the following dependency to your `project.clj` file:

```clojure
[khroma "0.1.0"]
```

## Usage Example

```clojure
(ns example
  (:require [khroma.runtime :as runtime))
  
  
; receieve messages for extension  
(let [messages (runtime/on-message)]
  (go-loop [] 
    (when-let [message (<! messages)]
      (process-message message)
      (recur)))
      
; send message to anoher extension      
(runtime/send-message 
   {:message-data "xx" :something-else "yyy"}
   {:extensionId "some.other.extension"
    :responseCallback 
      (fn [response]
        (handle-response response))})
```




## License

Copyright © 2015 SUPREMATIC (http://www.suprematic.net)

Distributed under the Eclipse Public License, the same as Clojure.
