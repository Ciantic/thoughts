# WordPress Gutenberg experience notes

I've long hold out on switching to Gutenberg, the block layout editor of WordPress. Mostly because it was rather half baked few years ago when I last tried. I'm now using it, and plan to use it, but it's still amazing how many things are still half-assed.

Look no further than the most basic image block, it has [hilarious issue thread from 2018, and still open!](https://github.com/WordPress/gutenberg/issues/12168) It's full of screenshots of broken behavior. People don't know seem to grog even what the percentage buttons are supposed to mean, and consequently the image breaks out of it's container or image gets out of aspect ratio.

I also noticed that 100% toggle button is by default pressed, yet if I press it again the image changes size. What? That's not how toggle buttons supposed to work but what ever. Looks like whoever did the image block half-assed it by trying to add too many features which end up breaking it.

Other pain point is that I really like types and type-safe code. TypeScript support is somewhat functional with Gutenberg, but sure enough after few weeks of trying I've already found missing functions and unqualified types in the type definitions.

Registration of blocks is a mess of JSON/JS/PHP files. In the end if you want type-safe code you have to write TypeScript types for attributes, PHP types for attributes, and then duplicate the attribute definitions to JSON.

WordPress is aging tech stack, and it really shows in Gutenberg experience. It's slightly akward to do React and then server side rendering again in PHP. I would not write most applications with it, but it's very suitable for regular websites.
