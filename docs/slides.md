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

_Why not a sub title?_

<footer>

2022 · Zurich · Stefan Huber

</footer>

--s--

https://raw.githubusercontent.com/signalwerk/blog.learnings/main/js-fails.md

source: https://liip.slack.com/archives/C02K3G9US/p1647252397862119

Oh gosh... I had a weird Bug and couldn't find it, but now I figure it out: Summer time (Daylight saving) is coming up on Sunday, 27 March and I made wrong assumptions...
I always make the same mistakes...

## Question

What are your top 3 causes of bugs you write? And how do you avoid it?
((See thread for mine)) (edited)

Here are my top 3 causes of bugs I usually write:

- _Problem_: Access non existing keys in an object `obj.test` _Solution_: `obj?.test` or `obj && obj.test` (TS for the win)
- _Problem_: Date & Time stuff. _Solution_: I try to work with timestamps (int) and if not possible I try to work with UTC-Time for calculation. Most of the time I realise `moment.js` would have saved me but I usually don't take it because it's just a huge dependency in terms of file-size in the browser.
- _Problem_: recursion. _Solution_: try whenever possible to do it in loops.

--s--

```fm
style: negative
background: true
```

## exit 0; thx

# Questions?
