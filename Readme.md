# ng2-simple-timer

A simple timer service for Angular 2, base on RxJS.

Name/ID(string) base API. RxJS object not exposed.

## Index
<!-- TOC -->

- [Install](#install)
- [Usage](#usage)
	- [Import into Angular 2 application (typescript)](#import-into-angular-2-application-typescript)
	- [API](#api)
		- [newTimer](#newtimername-string-sec-number-boolean)
		- [delTimer](#deltimername-string-boolean)
		- [getTimer](#gettimer-string)
		- [getSubscription](#getsubscription-string)
		- [subscribe](#subscribename-string-callback-any-void-string)
		- [unsubscribe](#unsubscribeid-string-boolean)
- [Example](#example)
- [Contributors](#contributors)
- [Changelog](#changelog)
- [License](#license)

<!-- /TOC -->
## Install

```
npm install ng2-simple-timer
```

## Usage

### Import into Angular 2 application (typescript)

ng2-simple-timer is implemented as Angular 2 injectable service name __SimpleTimer__.

```javascript
import {SimpleTimer} from 'ng2-simple-timer';
```

Add SimpleTimer into providers in your top level component (eg. [app.component.ts](https://github.com/J-Siu/ng2-simple-timer-example/blob/master/app/app.component.ts)).

__Do not add to providers of child component!__

```javascript
@Component({
	'selector': 'app-component',
	'template': `...`,
	'providers': [SimpleTimer]
})
```

For each child component require SimpleTimer, add to constructor.

```javascript
constructor(private st: SimpleTimer) { }
```

### API

##### newTimer(name: string, sec: number): boolean

`newTimer` will create timer `name` and tick every 'number' of seconds. Creating timer with the same name multiple times has no side effect.

Return `false` if timer `name` exist.

```javascript
this.st.newTimer('5sec', 5);
```

##### delTimer(name: string): boolean

`delTimer` will delete timer `name`

Return `false` if timer `name` does not exist.

```javascript
this.st.delTimer('5sec');
```

##### getTimer(): string[]

`getTimer` will return all timer name in string array.
```javascript
let t: string[] = this.st.getTimer();
```


##### getSubscription(): string[]

`getSubscription` will return all subscription id in string array.
```javascript
let ids: string[] = this.st.getSubscription();
```


##### subscribe(name: string, callback: (any) => void): string

`subscribe` will link `callback` function to timer `name`. Whenever timer `name` tick, `callback` will be invoked. 

Return subscription id(string).

Return empty string if timer `name` does not exist.

Either use Lambda(fat arrow) in typescript to pass in callback or bind `this` to another variable in javascript, else `this` scope will be lost.

__Lambda(fat arrow)__
```javascript
counter: number = 0;
timerId: string;

ngOnInit() {
	// lazy mode
	this.timerId = this.st.subscribe('5sec', e => this.callback());
}

callback() {
	this.counter++;
}
```


##### unsubscribe(id: string): boolean

`unsubscribe` will cancel subscription using `id`.

`unsubscribe` will return false if `id` is undefined or `id` is not found in subscription list.

```javascript
timerId: string;

this.st.unsubscribe(this.timerId);
```


## Example

[ng2-simple-timer-example](https://github.com/J-Siu/ng2-simple-timer-example)


## Contributors

* John Sing Dao Siu (<john.sd.siu@gmail.com>)


## Changelog

* 0.2.0
* 0.2.2
	- API change
		- newTimer() return boolean
		- subscribe() - lazy mode removed
	- API new
		- delTimer() 

## License

The MIT License

Copyright (c) 2016

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.


