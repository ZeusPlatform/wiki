```js
import { EventEmitter } from 'events'

class HelloEmitter extends EventEmitter {
  hello () {
    console.log(this.listeners('hello'))
  }
}

const a = new HelloEmitter()
a.on('hello', () => {})

a.good()

```