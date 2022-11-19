# Digital Garden Design and Implementation Notes

## The Technical 

Spent a day evaluating ways to share my garden beyond giving people a link to
the github repo (which is still on the table BTW). There's a class of software
that translates markdown-html while providing indexes, styling, and everything
else we expect from a "modern" personal web site. After trying out
[Pelican](https://getpelican.com/), [hugo](https://getpelican.com/),
[zola](https://www.getzola.org/documentation/getting-started/overview/), and
[mkDocs](https://www.mkdocs.org/), I ended up with mkDocs. Which makes my brain
look like an open-source project, and I guess it is.

The primary technical annoyance is that most of my note-taking and note-reading happens 
in the editor. So preserving folder structure and ability to follow links in-editor 
were both important. Pelican converts folder hierarchies into category tags. Both hugo and zola required additional work to get into deep trees. mkDocs respected folder hierarchy and gave me what I was about to create for myself with three lines of config:

```yaml
site_name: My Mental Rummage Sale
site_url: https://example.com/
theme: readthedocs
```

## Philosophical

A lot of this is converging on Tom Critchlow's ideas regarding [gardens, streams, and campfires](https://tomcritchlow.com/2018/10/10/of-gardens-and-wikis/). Some of the 
problems with the design of social media include:

* Unmoderated spaces tend to favor the loudest and most aggressive voices. This is
an effect we've studied since the 90s. 
* Conversely, "hot takes" get more views, which in turn get more boosts.
* Social pressure to perform on a daily or weekly basis. 
* The relationship between ephemera and creative work gets inverted. We archive
ephemeral ideas for decades while more reflective work gets buried and lost.

I have a bit of bias here. I'm a recovering social media addict, so I need to be
extremely careful about how and what I post online. The problem with "someone's
wrong on the internet" rage is that someone is always wrong on the internet. And
it's easy to get stuck fighting the same arguments online your friends and
family have already agreed to disagree on. I had an anonymous blog (in hugo) for years 
and eventually killed it because while some ideas were good, others made me 
actively uncomfortable after life changed my perspective. 

At the same time, I recognize the value of getting work out there, even imperfect
work. 

So anyway, trying out a digital garden where anything can be pruned. Most of it won't 
be interesting, and the piles of dirt, wheelbarrows, and paving stones are conspicuously visible. People who want more day-to-day stream-like stuff can find me on any of the smaller communities I feel comfortable engaging in. 


---


* first draft: 2022-11-19

