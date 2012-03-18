Why we need Python in the Browser
=================================

In his `Pycon 2012 <https://us.pycon.org/2012/>`_  keynote speech on Sunday, Guido van Rossum covered many of the open “Troll” questions related to the Python community. I’ve had occasion to either complain about or defend all of the topics he covered, and he did a wonderful job of addressing them. The issues could largely be divided into two categories: those that come from a fundamental misunderstanding of why Python is wonderful (e.g. whitespace), and those that are not an issue for the core python dev team, but are being actively worked on outside of core Python (e.g event loop).

And then there’s the question of supporting Python in the web browser. I honestly thought I was the only one that cared about this issue, but apparently enough people have complained about it that Guido felt a need to address it. His basic assertion is that the browsers aren’t going to support this because nobody uses it and that nobody uses it because the browsers don’t support it.

This is a political problem. Politics shouldn’t impact technical awesomeness.

The fallacious underlying assumption here is that modern HTML applications must be supported on all web browsers in order to be useful. This is no longer true. Web browser applications are not necessarily deployed to myriad unknown clients. In a way, HTML 5, CSS 3, and DOM manipulation have emerged as a de facto standard MVC and GUI system. For example, many mobile apps are developed with HTML 5 interfaces that are rendered by a packaged web library rather than an unknown browser. Client side local storage has created fully Javascript applications that require no or optional network connectivity. There are even situations where it may not be necessary to sandbox the code because it’s trusted. Many developers create personal or private projects using HTMl 5 because it’s convenient.

Convenient. It would be more convenient if we could code these projects in Python. Web browsers can be viewed as a zero install interface, a virtual machine for these applications. Such a VM has no reason to be language dependent.

It is simply unfair to all the other programming languages and coders of those languages to say, “we can’t displace Javascript, so we won’t try.” Web browsers have evolved into a virtualization layer more like operating systems than single programs. While it is true that the most restrictive operating systems only permit us to code in Objective C, in general, it is not considerate to restrict your developers a single language or environment.

It is time (in fact, long overdue) for Python to be supported in the browser, not necessarily as an equal to Javascript, but as an alternative. The web is a platform, and we must take Guido’s statement as a call to improve this platform, not to give up on it.

Update: I just stumbled across http://www.gnu.org/software/pythonwebkit/ and I can’t wait to play with it!

Update 2: From the number of comments on this article, it appears that my article has hit some web aggregator. To those users suggesting python to javascript compilers, I’ve been a `minor contributor <http://archlinux.me/dusty/tag/pyjaco/>`_  to the `pyjaco <http://pyjaco.org/>`_  project, a rewrite of the pyjs library. It has the potential to be a great tool, and the head developer, Christian Iversen is very open to outside contributions. Let’s make it better!