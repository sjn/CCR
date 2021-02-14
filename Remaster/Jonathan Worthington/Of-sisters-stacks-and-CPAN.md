# Of sisters, stacks, and CPAN
    
*Originally published on [2018-01-26](https://6guts.wordpress.com/2018/01/26/of-sisters-stacks-and-cpan/) by Jonathan Worthington.*

Recently, an [open letter](https://www.perl.com/article/an-open-letter-to-the-perl-community/) was published by *Elizabeth Mattijsen*, a long-time contributor to the Perl community who has in recent years contributed copiously to Rakudo Perl 6, as well as working to promote Perl (both 5 and 6) at numerous events. The letter made a number of points, some of them yielding decidedly unhappy responses. I’ve been asked a number of times by now for my take on the letter and, having had time to consider things, I’ve decided to write up my own thoughts on the issues at hand.

### Oh sister

A number of years back, I played a part in forming the “sister language narrative”. The reality – then and now – is that both Perl and Perl 6 have userbases invested in them and a team willing to develop the languages and their implementations. These userbases partly overlap, and partly consist of people with an interest in only one or the other.

Following the Perl mantra that “there’s more than one way to do it”, I saw then – and see now – no reason for the advent of Perl 6 to impose an “end of life” on Perl. During the many years that Perl 6 took to converge on a stable language release with a production-ready implementation, Perl continued to evolve to better serve its userbase. And again, I see no reason why it should not continue to do so. For one, Perl 6 is not a drop-in replacement for Perl, and it’s unreasonable to expect everyone using Perl today to have a business case for migrating their existing systems to use Perl 6. When there’s a team eager to carry Perl forwards, what’s to lose in continuing to work towards serving that Perl userbase better? Caring about and supporting an existing userbase is a sign of a mature language development community. It shows that we’re not about “move fast and break stuff”, but “you can trust us with your stuff”.

Moreover, it’s very much the case that Perl and Perl 6 make different trade-offs. To pick one concrete example, Perl 6 makes it easy to run code across multiple threads, and even uses multiple threads internally (for example, performing optimization and JIT compilation on a background thread). Which is great…except the only winning move in a game involving both threads and ``fork`` is not to play. Sometimes one just can’t have their cake and eat it, and if you’re wanting a language that more directly gives you your POSIX, that’s probably always going to be a strength of Perl over Perl 6.

For these reasons and more, it was clear to me that the best way forward was to simply accept, and rejoice in, the Perl community having multiple actively developed languages to offer the world. So where did the sister language narrative come in?

The number 6 happens to be a larger number than 5, and this carries some implications. I guess at the outset of the Perl 6 project, it was indeed imagined that Perl 6 would be a successor to Perl. By now, it’s instead like – if you’ll excuse me a beer analogy – Rochefort 8 and Rochefort 10: both excellent beers, from the same brewery, who have no reason to stop producing the 8 simply because they produce the 10. I buy both, and they’re obviously related, though different, and of course I have my preference, but I’m glad they both exist.

The point of the “sister language” narrative was to encourage those involved with Perl and Perl 6 to acknowledge that both languages will continue to move forward, and to choose their words and actions so as to reflect this.

I continue to support this narrative, both in a personal capacity, and as the Rakudo Perl 6 Pumpking. (For those curious, “pumpking” is a cute Perl-y word for “project leader”, although one could be forgiven for guessing it means “flatulent monarch”.) Therefore, I will continue to choose *my* words and actions so as to support it, unless a new consensus with equally broad community buy-in comes to replace it.

I accept that this narrative may not be perfect for everyone, but it has been quite effective in encouraging those who feel strongly about just Perl or just Perl 6 to focus their efforts constructively on building things, rather than trying to tear down the work of others. Therefore, it was no surprise to me that, when Liz’s open letter and follow-up comments went against that narrative, the consequences were anything but constructive.

I can’t, and don’t feel I should try to, control the views of others who contribute to Perl 6. Within reason, a diversity of views is part of a healthy community. I do, however, have a few things to ask of everyone. Firstly, when expressing a view that is known not to have widespread community consensus, please go to some lengths to make it clear it is a personal position. Secondly, when reading somebody’s expressed position on a matter, don’t assume it is anything more than *their* position unless clearly stated. And – perhaps most importantly – please also go to lengths to discuss topics calmly and politely. I was deeply disappointed by the tone of many of the discussions I saw taking place over the last week. We can do better.

### Perl on the Rakudo stack?

The next section of the letter considered the possibility of a “Butterfly Perl” project: effectively, a port of Perl to run atop of the Rakudo stack (in reality, this doesn’t involve Rakudo much at all, but rather NQP and MoarVM). As a compiler geek, this of course piques my interest, because what could be more fun that writing a compiler? :-) And before anyone gets excited – no, I don’t have the time to work on such a thing. But, in common with *Liz*, I’d be supportive of anyone wishing to experiment in that direction. There will be some deep challenges, and I’ll issue my usual warning that syntax is what gets all the attention but semantics are what will eat you alive.

Where I will disagree, however, is on the idea of a moratorium on new features in Perl. These appear slowly anyway (not because Perl Porters are inefficient, but because adding new features to such a widely used language with a 30-year-old runtime is just a really darn hard thing to be doing). Given the immense technical challenges a Perl-on-new-VM effort would already face, the odd new feature would be a drop in the bucket.

My one piece of unsolicited advice to those working on Perl would be to borrow features from Perl 6 very carefully, because they are generally predicated on a different type system and many other details that differ between the Perls. (My diagnosis of why smartmatch has presented such a challenge in Perl is because it was designed assuming various aspects of the Perl 6 type system, which don’t map neatly to Perl. This isn’t surprising, given Perl 6 very consciously set out to do differently here.) But should Perl simply stop exploring ways to make things better for is userbase? No, I don’t think so. From a Perl user point of view (which is the only one I have), adding subroutine signatures – which deliver existing semantics with less boilerplate – feels like a sensible thing to do. And adding features to keep up with the needs of the latest versions of the Unicode specification is a no-brainer. “Perl (5 or 6) is great at Unicode” is a meme that helps us all.

### The CPAN butterfly plan

The final part of the letter proposes a focused porting effort of Perl modules to Perl 6. This idea has my support. While the Perl 6 module ecosystem has been growing – and that’s wonderful – there’s still a good number of things missing. Efforts to address that expands the range of tasks to which Perl 6 can be conveniently applied. Of course, one can reach such modules already with the excellent `Inline::Perl5` too. Some folks have reservations about dual runtimes in production, however, and interop between two runtimes has some marshalling cost – although with recent optimization work, the cost has been brought well down from what it was.

Of course, in some areas it’s strategic to build something afresh that takes into account the opportunities offered by Perl 6. That’s why I designed Cro by reading RFCs and considering the best way to implement them in Perl 6. Even then, I did it with the benefit of 20 years experience doing web stuff – without which, I suspect the result would have been rather less useful. Porting existing modules – taking time to tweak their APIs to feel more comfortable in Perl 6 – means that existing knowledge built up by the authors of those modules can be carried forward, which is surely a win.

### In closing

I’ve had the privilege of working with *Liz* for a number of years. While her open letter makes a number of points I disagree with, I have no reason to believe it wasn’t written out of good intentions. Some people have wondered if any good can come of it. That’s up to us as a community. I think we can, at least, take away:

- A reminder of the importance that the “sister language” narrative plays in our community. This should encourage all of us to – at the very least – quietly tolerate it.
- Further evidence that the only way that narrative will be replaced is by following the same path that created it: through quiet, thoughtful, discussions with all major stakeholders, to reach a consensus.
- That a Perl atop of NQP/MoarVM effort – should anybody wish to try it – will receive some support. As I’ve noted, the technical challenges are considerable, and deep. But they were for implementing Perl 6 too, and we’ve managed that. :-)
- A much-needed injection of energy into increasing the number of modules in the Perl 6 ecosytem, taking inspiration from (and so hopefully avoiding mistakes already made and rectified by) Perl modules.

And, last but not least, it has been clear that – while it has in the last days often been expressed in raw and heated ways – we, as the Perl community, have two languages we’re passionate about and are keen to drive forward. Let’s do that together, in peace, not in pieces.