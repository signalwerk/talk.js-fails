---
theme: signalwerk
title: My top three JavaScript errors
---

```fm
style: negative
background: true
```

## Hello _👋_

# {{process.content.frontmatter.title}}

_And how to avoid them?_

<footer>

2022 · Zurich · Stefan Huber

</footer>

--s--

## Thank you Thor _🫶_


- Try to show how to **avoid** my errors
- Try it in **5 min**
- Based on a [Slack-Message](https://liip.slack.com/archives/C02K3G9US/p1647252397862119) from 14th March 2022

--s--

```fm
style: negative
background: true
```

## looks simple, is dangerous

# _💣_ Recursion

--s--

## _🤬_ uff...

# It's not even easy to explain…

--s--

## Example – walker

```html
<div>
  <p class="hello">world</p>
  <div>
    <p class="hello">world</p>
  </div>
</div>
```

--s--

## Example – walker

```js
function walkDOM(node) {
  do {
    node.classList?.remove("hello");
    if (node.hasChildNodes()) {
      walkDOM(node.firstChild);
    }
  } while ((node = node.nextSibling));
}
```

--s--

## Example – array

```js
const work = [1, 2, 3, 4];

function recursionSummary([item, ...rest]) {
  if (!rest.length) {
    return item;
  }
  return item + recursionSummary(rest);
}

recursionSummary(work);
```

--s--

## Problems with recursions

- Maximum call _stack size_ exceeded
- _depth-first_ vs. _breadth-first_ problems
- _access to parent_ nodes
- _return to parent_ caller

--s--

```fm
style: negative
background: true
```

## &nbsp;

# How to avoid?

--s--

## well...

# try to _«unroll»_ the recursion

--s--

## Examples

<div style="font-size: .85em">

---

```js
function reducderSummary(work) {
  return work.reduce((acc, item) => acc + item, 0);
}
```

---

```js
[...document.querySelectorAll(".hello")].map((node) => {
  node.classList.remove("hello");
});
```

> Most of the time: if the recursion is at the end of a function call, there is something wrong (tail recursion).

</div>

--s--

```fm
style: negative
background: true
```

## The winner is…

# _💥_ reference to <br>undefined property

--s--

## Example – okish

```js
const car = {
  wheels: 4,
};
```

---

```js
const passenger = car.passenger; // = undefined
```

--s--

## Example – error

```js
const car = {
  wheels: 4,
};
```

---

```js
const passenger = car.passenger; // = undefined
const gender = car.passenger.gender;
// 💥 TypeError:
// Cannot read properties of undefined
// ≈ undefined.gender
```

--s--

```fm
style: negative
background: true
```

## &nbsp;

# How to avoid?

--s--

## «Old» JavaScript

<div style="font-size: .85em">

```js
import { get } from "underscore";

const gender = get(car, "passenger.gender");
// = undefined
```

---

```js
const gender = car && car.passenger && car.passenger.gender;
// = undefined
```

</div>

--s--

## «New» JavaScript

- Use _optional chaining_ with `?.` (nullsafe operator)
- Use typed languages like _TypeScript_ or _Flow_

---

```js
const gender = car?.passenger?.gender;
// = undefined
```

--s--

```fm
style: negative
background: true
```

## It is simply not simple

# _🧨_ Date & Time stuff

--s--

## Example – error

<div style="font-size: .85em">

```js
const now = Date.now(); // unix timestamp im ms
const tomorrow = new Date(now + 24 * 60 * 60 * 1000);
const nextYear = new Date(now + 365 * 24 * 60 * 60 * 1000);
```

</div>

> Assumes a day is having <br>*24 h 0 min 0 sec 0 ms* <br>and a year has <br>*365 days*

--s--

## _Days_ – wrong assumptions

- A day is having _24 h 0 min 0 sec 0 ms_ <br> **wrong:** daylight saving
- Your logs don't have _leap seconds_ <br> **wrong:** sometimes leap seconds

--s--

## _Timezones_ – wrong assumptions

- The client is in the same _time zone_ as the server <br> **wrong:** time zones are different
- Your problems will disappear if you _convert_ to UTC or use Unixtimestamps<br> **wrong:** you will make other mistakes
- Timezones are only off by _full hours_ <br> **wrong:** time zones are also off by 30 min or 45 min
- Timezones are _bound to a location_ <br> **wrong:** for some events they change

--s--

## _Years_ – wrong assumptions

- A year is having _365 days_ <br> **wrong:** leap years
- _Public holidays_ are easy and you know the rules <br> **wrong:** public holidays are political/religous and moving
- _Age_ calculation is easy <br> **wrong:** different cultures different ages – see: [Korean age system](https://en.wikipedia.org/wiki/East_Asian_age_reckoning)

--s--

## In general

# If you think in your case it doesn't matter; <br>_you are most likeley wrong_

--s--

```fm
style: negative
background: true
```

## &nbsp;

# How to avoid?

--s--

## hmm... 🤔

# use a _library_!

- check [moment.js](https://momentjs.com/) or [Luxon](https://moment.github.io/luxon/)

```js
const tomorrow = moment().utc().add(1, "day");
const nextYear = moment().utc().add(1, "year");
```

--s--

```fm
style: negative
background: true
```

## exit 0; thx

# Questions?
