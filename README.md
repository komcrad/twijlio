# twijlio

A Twilio REST API client

This uses the twilio rest api documented here: https://www.twilio.com/docs/api/rest

[![Clojars Project](https://img.shields.io/clojars/v/twijlio.svg)](https://clojars.org/twijlio)

## Usage

By default, twijlio will look at your environment for auth credentials:
```
TWILIO_ACCOUNT_SID=AC...
TWILIO_AUTH_TOKEN=5f4dcc3b5aa765d61d8327deb882cf99
```

Or set your auth credentials:
```clojure
(require [twijlio.config :as config])

(config/set-account-auth! {:account-sid "AC..." :auth-token "5f4dcc3b5aa765d61d8327deb882cf99"})
```

Send an SMS to (505) 555-1212 from your twilio number (888) 555-2211 with your coolest smiley face.
```clojure
(require [twijlio :as tw])

(tw/send-message "+15055551212" "+18885552211" {:Body "Hey Buddy <(^_^<)"})
```

Send an MMS to (101) 555-1212 from your twilio number (999) 555-1122 with a gif of your new AI.

```clojure
(tw/send-message "+11015551212" "+19995551122" 
	{:MediaURL "https://i.imgur.com/vnvIZ.gif" :Body "Check out Tayne!"})
```

Make a call to (202) 555-1212 from your twilio number (800) 555-2121 and [say hello](https://www.twilio.com/labs/twimlets/message).

```clojure
(tw/make-call "+12025551212" "+18004442121" 
	{:Url "http://twimlets.com/message?Message%5B0%5D=Hello%2C%20World!&"})
```

## Advanced Usage

Use different account temporarily
```clojure
(require [twijlio.config :as config])

(config/with-account {:account-sid "AC..." :auth-token "5f4dcc3b5aa765d61d8327deb882cf99"} (tw/make-call "+19005552121" "+13035551212"))
```

Operate on a subaccount
```clojure
(require [twijlio.config :as config])

(config/with-target-sid "AC12345678901234567890123456789012" (get-calls))
```

## Thanks

Heavily based on [rwillig/clj-dispatch.me](https://github.com/rwillig/clj-dispatch.me). Thanks Ray!

## License

```
MIT License

Copyright (c) 2016 weekdayfabian

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```
