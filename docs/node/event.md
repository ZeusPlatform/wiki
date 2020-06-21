```js
import { EventEmitter } from 'events'

class HelloEmitter extends EventEmitter {
  hello () {
    console.log(this.listeners('hello'))
  }
}

const a = new HelloEmitter()
a.on('hello', () => {console.log('hello')})

a.hello()
a.emit('hello')

```