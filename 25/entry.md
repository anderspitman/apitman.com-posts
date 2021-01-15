I have a project idea that could involve doing some scraping of YouTube videos, so I started poking
around the HTML output of curling YT links. These things are a site (sp) to behold. If you curl the following
well-known URL and store it in a file:

`https://www.youtube.com/watch?v=dQw4w9WgXcQ`

Just searching for the title yields 14 results, spread throughout random HTML and JS. But it's only actually
displayed to the user once on the page, and probably again in the browser tab. It's not just the title
either, there's a ton of duplicated data and bloat throughout the file. I'm guessing it compresses well. I
checked a few other files and they all had between 10 and 18 copies of the title.

I'm not sure what conclusions to draw from this. A lot of them are obviously intended to be
machine-readable for things like [ogp][0], but do you really need 14 identical copies?

EDIT:

Since this errant observation somehow made it to the [Hacker News front page][1], and eventually got flagged, I have a few more thoughts:

* Sorry the title ended up more clickbatey than intended. It's not making 14 extra HTTP requests just for the title. It originally started with "An HTTP request" but it was a few characters too long for HN, and I didn't spend much time rethinking it.

* I agree the extra text isn't a problem (like I said, that'll compress well). I'm more concerned about the underlying complexity it signals. There is more obvious evidence of this complexity (it makes 70 network requests when you load the page even if you pause the video immediately), this is just a novel one for me.

* I appreciate the copies which are intended to interoperate with other systems like Twitter and OGP.

* I actually appreciate the fact that a JSON blob of all the video metadata is embedded in the HTML. It'll make my scraping task much simpler.

[0]: https://ogp.me/

[1]: https://news.ycombinator.com/item?id=24631698