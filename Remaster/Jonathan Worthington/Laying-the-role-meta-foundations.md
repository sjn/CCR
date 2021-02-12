# Laying the role meta-foundations
    
*Originally published on [25 November 2009](https://use-perl.github.io/user/JonathanWorthington/journal/39943/) by Jonathan Worthington.*

I got back from Latvia yesterday. The first Baltic Perl Workshop was very small, but also very enjoyable. I also very much enjoyed meeting up with *masak*++, who shares my love of good food - curry included! Riga turned out to be a great place for having a good nom, both in terms of local stuff and nice hot curry. And of course, amongst the workshop and some sightseeing, some hacking got done too.

Today was Rakudo Day, and it was time to get back to meta-model matters. I actually spent a while during my time in Riga reading a good bit of Moose and Class::MOP - I'd seen bits of them before, but this time gave the parts relating to roles a much closer look and got myself a refresher on some other bits. I also spent the plane ride home (pretty much the entire flight!) reading an interesting paper on [composing meta-objects from traits](http://scg.unibe.ch/archive/papers/Duca05ySafeMetaclassTrait.pdf), which turned out to be a much easier read than I had expected, but left me wanting to read many of its references too.

The first thing I worked on today was getting more details into [metamodel.pod](http://github.com/rakudo/rakudo/blob/ng/docs/metamodel.pod), which is the currently under heavy construction specification for Rakudo's meta-model. It will in the future become a proposal for inclusion in the Raku specification too, at which point it'll be time to co-ordinate with other implementations to get something that we can all agree on. Anyway, if you have an interest in meta-programming, you may be interested to give it a read and leave comments, or catch me on #raku. For those just wanting to see some code rather than read a spec, skip straight down to the example of how writing a module to support something AOP-ish could look. It'll no doubt evolve somewhat, and we won't be able to run it for a little bit yet, but I think it's a nice example of how easy it should be to implement such things in Raku.

After that, I dug into starting to get some implementation work done, with a focus on working towards having role composition working as spec'd in the metamodel document. So far I've got a lot of the foundations laid, and I'm now starting to build up on them. So far, it's mostly just plumbing, but composing a role into a class and the class then gaining the role's methods does now work, and a bunch of what we need for required methods and conflict resolution is stubbed in, though untested. I also was able to write a chunk of this in NQP rather than PIR, something I'd like to see us increasingly do in the stage 1 compiler, where it makes sense to do so (the stage 1 compiler containing the things we need in order to compile the setting; the smaller we can keep this part, the better it'll be for us overall...for now the goal is mostly getting the ng branch landed rather than small-stage-1-nirvana though :-)). Anyway, I think I can probably progress pretty fast from here and get our role stuff up and running in the next couple of days.

Thanks to Vienna.pm for sponsoring Rakudo Day.