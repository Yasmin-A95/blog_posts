# Making the Web Developers Pilgrimage

Jens Oliver describes reading the HTML specification as the Web Developer's Pilgrimage. As a Junior Web Developer who sees herself specialising in the front end long-term, it's time for me to make the journey. 

For a look at the scope of this pilgrimage, scroll all the way to the bottom and back up again of the one-page version. Even the table of contents is a hefty thing. I guess they made the CSS hideous just for funsies. A look under the hood of the page immediately revealed a HTML tag I've never heard of before so that's fun. Feast your eyes on... 
```html
<header id="head" class="head with buttons">
    <a class="logo" href="#">
        <img alt="WHATWG" crossorigin="" src="#" width="100" height="100">
    </a>
    <hgroup>
        <h1 class="allcaps">HTML</h1>
        <h2 id="living-standard" class="no-num no-toc">
            Living Standard — Last Updated
            <span class="pubdate">17 October 2022</span>
        </h2>
    </hgroup>
</header>
```
Note: I substituted the src and href values for a hash so it would fit more nicely on this page.

Looky look at `<hgroup>` that's a new one for me. Likewise with `crossorigin=""`. A bit of reading into it indicates that setting the cross-origin blank `crossorigin=""` is a way to specify an anonymous cross-origin. More reading into why you'd want or need this is necessary, but I don't want to fall into too many rabbit holes when I'm already undertaking a huge adventure through HTML. No sidequests today.  

On that note.

### Read It Like This

From the spec itself, "This specification should be read like all other specifications. First, it should be read cover-to-cover, multiple times. Then, it should be read backwards at least once. Then it should be read by picking random sections from the contents list and following all the cross-references.” 

Jens, the person who's article gave me this grand plan, says "As HTML is the most important language on the Web, and as this—reading, reviewing, feeding back on [2,182 pages about HTML](https://docs.google.com/gview?url=https://html.spec.whatwg.org/print.pdf&hl=en) —is such an epic endeavor, we may call this the Web Developer’s Pilgrimage. *I* call this the Web Developer’s Pilgrimage—and I recommend every web developer, and especially every frontend developer, to make it.
...Web professionals, standing on the shoulders of giants. Start and write about your HTML pilgrimage!"

Well, alright then. 

### Thoughts and Findings 

#### Section 1.6 - History



###### WHATWG Spicy Eddition 

It gets scathing pretty much immediately, which I love. Who'd have expected it to be spicy? The dish: HTML5 is a buzzword. Thank god for that. I'd heard it thrown around or required in job ads and felt like I was missing important context in the way a lot of lofty words inspire. It largely refers to modern web technologies, "many of which developed at the Web Hypertext Application Technology Working Group (WHATWG)". One of their projects is the HTML standard specification. Nice self-plug guys. 

###### HTML Lore 

A nice bit of HTML lore is that it, along with the internet at large, has its origins as a means of semantically describing (HTML) and hosting (Web) scientific papers. It's luckily that its general design over the years enables us to put it to use in a much much wider range of contexts, and usage has extended out from academic institutions and into the hands of us more common folk. Now It's our turn to keep passing it down the chain and doing the work required to hand it over to the leagues of people still squeezed out by one means or another. I did say no sidequests today, but this one is **the most important.** 

###### XHTML 

In 1998, the year Frank Sinatra (famous inventor of the Ruby Framework 'Sinatra') tragically died, humanities wandering eyes turned from HTML to an XML equivalent. It didn't take all that well though, and today XHTML functionality isn't steadfastly grounded. Its unique benefits might not be passed on to the user, as XHTML that isn't HTML compatible ought to be avoided in case of browsers not supporting it. Sorry XHTML and Y2K. Some of us really thought you were going to change the world forever once upon a time.

1998 was a big year for reasons less fleeting, the DOM was born. What's more newsish to me, the DOM is considered part of the HTML API. What a fancy fact to hold in my head forever. Everyone knows the best programmers hold all this stuff in their heads 100% of the time. How could anyone ever toy around with web development if they didn't specifically know the DOM is part of the HTML API??? They couldn't. Never ever. 

2004ish

WHATWG was born, parented by Apple, Mozilla, and Opera. They decided to commit themselves to a specification that matches real-life implementation. Not sure what the alternative would look like, so thanks for not just writing fan fiction about HTML I guess. Along with committing to describe real things, HTML4, XHTML1, and DOM2 HTML were grouped together under the one specification. A big happy retro web family. 
 
### Resources 

In order of mention.

- [HTML specification](https://html.spec.whatwg.org/multipage)
- [Jens Oliver's Web Developer's Pilgrimage article](https://meiert.com/en/blog/web-developer-pilgrimage/)
- [HTML specification one-page version](https://html.spec.whatwg.org/)
- [HTML specification table of contents](https://html.spec.whatwg.org/multipage/#toc-introduction)
- [CORS enabled image](https://developer.mozilla.org/en-US/docs/Web/HTML/CORS_enabled_image)
- [HTML attribute: crossorigin](https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes/crossorigin)
- [How to read the spec](https://html.spec.whatwg.org/multipage/introduction.html#how-to-read-this-specification)
- [Why to read the spec](https://meiert.com/en/blog/web-developer-pilgrimage/) (link to Jen's article again for emphasis)
- [HTML spec intro](https://html.spec.whatwg.org/multipage/introduction.html#introduction)
- [WHATWG standards overview](https://spec.whatwg.org/)
- [XHTML Wiki](https://en.wikipedia.org/wiki/XHTML)