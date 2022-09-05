---
layout: post
title: First Impressions of the HP Envy x360
date: 2020-12-30
updated: 2022-09-05
tags:
  - Computers
  - Setup
---

Greetings. This is a compilation of my thoughts on the 2020 model HP Envy x360 (specifically the 13-ay0009na). Granted, I've only had it for a couple of days now, so I'm sure I'll find plenty more bugbears down the line, but overall I think this is a very solid machine with some remarkable qualities. It's not perfect, but for me, it does seem to fit the "secondary" machine role I intended it for, and I feel that it could easily become the primary machine for some — this thing is *quick*.

My frame of reference for comparisons includes the original Surface Go (with its anaemic Pentium chip), a Clevo laptop with a full-fat 4770k *desktop chip*, and a 4.3 GHz 8700k equipped desktop. That desktop is my primary, "Jarvis", so it's no surprise that it's faster... but I will say it's not by much.

This will be informal, and the up-front TLDR is this: if you need a high performance machine in a portable and compact form factor (aka, a *laptop*), this is a *very* viable option... with some caveats.

I'll expand on that in due course, but first let's break up the wall of text with a photo of our subject.

![](/assets/laptop/IMG_20200815_162210.jpg)

> Remember, this is a 13" laptop, so while the images might make it look quite big, it's not actually *that* big.

So, the real reason to be interested in this laptop, and why I used such an awful title, are those two shiny red stickers in the bottom right. (I will be getting rid of those stickers in due course, because they *do* interfere with my hand when it's resting on the deck, but that's really neither here nor there.)

![](/assets/laptop/hwinfo.png)

AMD's new Zen 2 laptop CPUs are going to be a big draw for many; they're certainly what drew me.

I bought this with the Ryzen 4700U, though realistically a SKU with the 4500U is equally capable for most tasks. Since neither have SMT, you're looking at 8 cores in the 4700U vs 6 cores in the 4500U — not that big a difference unless you're a *heavy* multitasker. Honestly, at £999.99 (VAT inc.) for the 4700U vs £799.99 (VAT inc.) for the 4500U equipped models (remembering that we only get 3 SKUs in the UK, with an even more expensive one that just has more internal storage) then that performance improvement in multicore tasks is most definitely not worth it for the price uplift.

What was worth it, however, was the increase to 16 GB from a measly 8 GB and the increase from 256 GB internal storage to 512 GB. From what I've seen the 8 GB SKUs only come as single channel, which is dumb since that's going to hamper performance, albeit then a little easier to upgrade.

Well, "worth it" is relative, honestly it's still not quite equitable: you could purchase the cheaper SKU, then for parity you'd grab an 8 GB stick of 3200MHz SODIMM RAM, which should run around £30 to £40 depending on price fluctuations, and then you'd grab a larger M.2 drive, with HP using an Intel 660p 512 GB which runs a little under £70. If you did that then, well, you would be saving about £90, which is nice, and you could instead grab two 16 GB sticks and try your luck or go for an even larger M.2 drive, perhaps a full 1 TB. Oh, but you *would* need to install it all yourself, which would likely be a time-consuming and fiddly process, especially without an iFixit teardown. *Thanks, HP.*

[Edit: With later research it appears that the RAM is soldered and thus not upgradable. What a shame HP.]

Either way, as given with [CURRENT GLOBAL SITUATION] driving up laptop sales and by the fact that Zen 2 CPUs are really *just that good*, which SKU you get may end up decided on your behalf.

There's simply nothing in stock. Anywhere. Good luck finding anything modern and half-decent. (Though as I write this, it seems HP *literally just now* got more in stock on their UK site.)

...

But holy shit, Zen 2. Wow. All this power at 15W? FIFTEEN!? Honestly, I'm stunned.

Spoiler Warning: This *15W laptop chip* trails only *ever so slightly* behind a *95W desktop CPU*.

That's *insane*.

Compared to the Surface Go (which I bought intending to use like a tablet, and ended up practically daily driving) which has a venerable 6W Pentium chip, this thing *shreds*. And compared to a 17" Clevo with a *desktop* 4770k, this thing is *actually a laptop*. As in, I can use it on my *lap* comfortably *without worrying where the nearest power outlet is*. And it's also *faster* (outside of GPU compute). 🤯

AMD has made something truly special.

Now, I'm not really one for benchmarks, primarily because I'm of the opinion only two of these three make sense:

a) Purchase your hardware to run well for your software stack (can be inferred)
b) Purchase your hardware knowing you can make the software run well on it
c) Purchase your hardware since it runs well on unrelated software (i.e., random benchmarks)

But I still prepped a couple of things to show just a little bit about how speedy this is.

Now, whilst there isn't a huge amount of reporting for this chip in particular, the TLDR of Zen 2 performance is that AMD is finally matching Intel in all-round single-threaded performance.

This means that I can tick off both a) and b). Also, since a lot of the high performance software I run uses SIMD and tends to prefer AVX to SSE, I'm very happy to see excellent SIMD from Team Red. And, since many of you probably know me as "the \*\*\*\*ing C programmer", it probably comes to no surprise that I like to use SIMD here and there, so I'm glad to see it in full colours (AVX-512 bad lol).

If you really want benchmarks, you'll be better served elsewhere. What I've put together are based on the two performance critical use-cases for my current work:

- CPython/PyPy for computer algebra and a little bit of scientific/numerical compute
- SAT solvers written in C/C++ (though we're very limited by system memory here)

Python isn't the be-all, end-all of performance, but it sure is a language I use a *lot*. I don't do much numerical work, mostly I need it for computer algebra like workloads as I'm typically doing combinatorics for generating and counting chessboards and such patterns, but good `scipy` performance (mostly `numpy` and thus C FFI/DLL performance) helps when I do something numeric.

Oh, you want to see numbers? Well... okay, let's start off with a generic python benchmark.

For the sake of a quick, generic comparison, here's `pyperformance` running on the Envy and on my primary machine (my 8700k equipped beast, Jarvis). I couldn't be bothered with multiple runs to reduce jitter, so this isn't great experimentation, but this does give a good idea for how you're really able to use a laptop like this for quick and dirty "real work". So, how does it fare?

[pyperformance](https://pypi.org/project/pyperformance/):

| Benchmark               | Envy    | Jarvis  | The Envy is  |
|-------------------------|---------|---------|--------------|
| 2to3                    | 451 ms  | 401 ms  | 1.13x slower |
| chameleon               | 26.4 ms | 10.7 ms | 2.47x slower |
| chaos                   | 126 ms  | 119 ms  | 1.05x slower |
| crypto_pyaes            | 129 ms  | 116 ms  | 1.11x slower |
| django_template         | 51.6 ms | 59.0 ms | 1.14x faster |
| dulwich_log             | 86.3 ms | 76.2 ms | 1.13x slower |
| genshi_text             | 39.9 ms | 33.1 ms | 1.21x slower |
| genshi_xml              | 127 ms  | 76.8 ms | 1.66x slower |
| hexiom                  | 11.1 ms | 10.1 ms | 1.10x slower |
| json_loads              | 31.5 us | 28.8 us | 1.10x slower |
| logging_format          | 13.3 us | 12.7 us | 1.05x slower |
| logging_simple          | 12.0 us | 11.7 us | 1.03x slower |
| mako                    | 19.4 ms | 20.4 ms | 1.05x faster |
| meteor_contest          | 111 ms  | 117 ms  | 1.05x faster |
| nbody                   | 141 ms  | 146 ms  | 1.04x faster |
| pathlib                 | 262 ms  | 306 ms  | 1.17x faster |
| pickle                  | 13.3 us | 12.4 us | 1.07x slower |
| pickle_dict             | 29.9 us | 31.7 us | 1.06x faster |
| pickle_list             | 4.47 us | 4.88 us | 1.09x faster |
| pickle_pure_python      | 499 us  | 485 us  | 1.03x slower |
| pidigits                | 195 ms  | 203 ms  | 1.04x faster |
| pyflate                 | 806 ms  | 727 ms  | 1.11x slower |
| raytrace                | 508 ms  | 517 ms  | 1.02x faster |
| regex_compile           | 189 ms  | 181 ms  | 1.04x slower |
| regex_dna               | 215 ms  | 191 ms  | 1.13x slower |
| regex_effbot            | 2.81 ms | 3.14 ms | 1.12x faster |
| regex_v8                | 32.3 ms | 26.4 ms | 1.22x slower |
| richards                | 69.2 ms | 72.1 ms | 1.04x faster |
| scimark_fft             | 407 ms  | 388 ms  | 1.05x slower |
| scimark_lu              | 179 ms  | 163 ms  | 1.10x slower |
| scimark_monte_carlo     | 115 ms  | 108 ms  | 1.06x slower |
| scimark_sor             | 209 ms  | 215 ms  | 1.03x faster |
| scimark_sparse_mat_mult | 5.09 ms | 4.52 ms | 1.13x slower |
| spectral_norm           | 176 ms  | 150 ms  | 1.17x slower |
| sqlalchemy_declarative  | 156 ms  | 176 ms  | 1.13x faster |
| sqlalchemy_imperative   | 24.9 ms | 31.6 ms | 1.27x faster |
| sympy_sum               | 206 ms  | 228 ms  | 1.11x faster |
| sympy_str               | 327 ms  | 344 ms  | 1.05x faster |
| telco                   | 7.16 ms | 6.56 ms | 1.09x slower |
| tornado_http            | 256 ms  | 224 ms  | 1.14x slower |
| unpickle                | 18.4 us | 17.3 us | 1.07x slower |
| unpickle_list           | 5.11 us | 4.90 us | 1.04x slower |
| unpickle_pure_python    | 359 us  | 331 us  | 1.08x slower |
| xml_etree_parse         | 177 ms  | 157 ms  | 1.13x slower |
| xml_etree_iterparse     | 126 ms  | 109 ms  | 1.16x slower |
| xml_etree_generate      | 116 ms  | 111 ms  | 1.05x slower |
| xml_etree_process       | 91.5 ms | 83.4 ms | 1.10x slower |


Yo, wtf? Like, I know I said this chip was good, but there is really not much in it a lot of the time. *And* this table doesn't even include the 13 tests that had a *sub-1% difference*.

And... is... is that... is the Envy running *faster*???

While some of it will be down to run-to-run variance, honestly this just shows how capable the 4700U really is to be trading blows with the 8700k, which truly blows my mind.

Oh... and I forgot to mention...

I ran this benchmark with the Envy *on battery*.

WTF.

Again, I know Python isn't going to be *that* reflective of performance differences, but it does show how far Zen 2 has come in single-threaded performance. Now I don't have to give too much up if I want to quickly sanity check something with the Envy, or modify and rerun a calculation.

Speaking of calculations, how does the Envy fare on a recent one of mine? Y'know, counting fundamental symmetries under invariants for pairs of squares on a chessboard ♟️... real fun stuff.

| Test          | Envy   | Jarvis | The Envy is  |
|---------------|--------|--------|--------------|
| symmetries.py | 16.50s | 14.55s | 1.14x slower |
| verify.py     | 40.51s | 40.43s | 1.01x slower |

Yeah... The Envy is only a little slower for the super-speedy `symmetries.py`... and it's basically the same speed for the heavier `verify.py` that uses brute force to sanity check the results?

What do I even keep Jarvis around for anyway at this point???

...

Joking aside, this is great for me. My Surface Go takes a sedentary 44.96s for `symmetries.py`. That's almost three times longer! And `verify.py` takes 108s! Yikes!

Oh, and let's not forget that the 4700U has 8 physical cores, while the Pentium has just 2 cores (with hyper-threading). Add in that I only bought my Surface Go with 4 GB of RAM (and 32 GB eMMC storage, ouch) and you can see how it is trounced by calculations that the Envy handles with *ease*.

Now, I'm sure some will have their eyes glaze over at this because *eww Python*.

Okay, how about some C performance figures?

Let's use a dumb little single-threaded \#SAT solver I wrote. It's basically just a DPLL SAT solver modified to use lots of bitwise arithmetic to solve specifically for the N-Queens problem. Oh, but with really weak propagation, hence how slow it is. Couldn't be bothered to fix that, it's caused by a bug.

| Input | Envy    | Jarvis  | Envy is      |
|-------|---------|---------|--------------|
| N=10  | 0.344   | 0.297   | 1.16x slower |
| N=11  | 3.234   | 2.563   | 1.26x slower |
| N=12  | 28.922  | 23.484  | 1.23x slower |
| N=13  | 308.141 | 246.594 | 1.25x slower |

I only include the results from N=10 to N=13 since below that it solves too quickly to get accurate timings and above that takes almost an hour on Jarvis, and I'm lazy and want to finish-up. 😆

Fundamentally, what we are seeing here is how there are indeed relatively significant differences between the 4700U and the 8700k in these kinds of bitwise arithmetic and branch intensive programs... which I should inform you is how SAT solvers spend practically all their CPU cycles.

Now, some of this is the difference in clock speed. The Envy was boosting between 3.95 GHz and 4.02 GHz, whilst Jarvis was running at 4.29 GHz to 4.36 GHz. However, this only accounts for half the performance delta, and I suspect most of the remaining delta is mostly dominated by the subtle differences in branch & jump prediction and differences in how they hide cache read/write latency.

But I would also like to reiterate that this is *a 15W chip versus a 95W chip*.

Zen 2 is some seriously impressive work from AMD and TSMC's 7 nm is *shaming* Intel's 14 nm node.

I could carry on with talk of performance, but really it's just more of the same: the 4700U is an insane amount of processing power in a tiny and lightweight package. The rest of the performance specs reflect this: high speed NVMe SSD (by Intel, ironically), 3200MHz dual-channel RAM (with rather sloppy timings but oh well), Vega 8 graphics — not that I'd game on it but it's leagues better than Intel's integrated graphics on the Surface Go — which means video playback is *smooth*.

So with that out of the way, time to discuss the rest of the laptop. Namely, the part HP is responsible for.

And this is where I have quite a bit of criticism to give, since it's clear HP cut corners or didn't test the design for long sessions of use. Now I can complain and criticise until the cows come home, but the Envy does have some pretty sore sticking points, especially for developers and people with average or larger hands.

Case in point, the keyboard.

![](/assets/laptop/IMG_20200815_162304.jpg)

I'm sorry, HP, but WHAT ON EARTH IS THAT MONSTROSITY???

If you didn't notice earlier, HP decided that you don't need a dedicated backslash key, but should instead press the FUNCTION KEY AND THE L KEY. Oh, and I hope you don't slip, because the function key is right next to the Windows key, and guess what Windows + L has *always* done?

IT LOCKS THE MACHINE.

![A picture of Captain Jean-Luc Picard from Star Trek facepalming in exhasperation.](/assets/facepalm.jpeg)

Honestly, that's a pretty dumb mistake on HP's part, though at the same time they would need to completely redesign the layout to accommodate it.

And clearly they don't want to do that because if you didn't notice, the keyboard isn't *really* in a standard UK layout anyway. They just switched @ and \". And included £. At least we got that much. (Ironically, a proper UK layout would have a dedicated backslash key and a shorter left shift to compensate, which would solve my biggest gripe...)

Oh, and that column of Delete/Home/End/Page Up/Page Down on the right-hand side?

Don't worry.

*You definitely won't be constantly hitting them in mistake and either moving your cursor when you want to backspace or accidentally sending the machine to sleep when you want to delete...*

It's a shame, because otherwise the keyboard is really awesome, and I *really like it*.

I'm not going to say nonsense about key travel or actuation points because, well, I'll be frank...

I'm a heavy-handed typist and I bottom out the keys most of the time anyway. Can't help it. 🤷

But that means I'm glad to report that even for me, it remains rather quiet, and it feels *very nice*.

Shame about the wrist rest though.

Yep, time for another complaint. This relates to the overall design, so it's PHOTO TIME!

![](/assets/laptop/IMG_20200815_162504.jpg)

> I guess it's nice, but any sense of premium they were going for with their new logo is lost with all the fingerprints.

![](/assets/laptop/IMG_20200815_162534.jpg)

> You can see how they've raised the wristrest, which is nice... but then they didn't make it a smooth transition up.

![](/assets/laptop/IMG_20200816_172810.jpg)

> So you get two sharp edges around the entire wristrest! First the raised section, then the actual lip of the chassis!

![](/assets/laptop/IMG_20200816_172805.jpg)

> Look how little machining would be needed to give you a nice, gradual, smooth, premium roll over the top edge.

HP decided to go for this whole sharp edge aesthetic (they call it "gem cut"). I don't think it looks bad, though clearly it's quite the fingerprint magnet (because apparently this isn't a solved issue).

Unfortunately, they decided that this meant we couldn't have a nice and smooth lip to the wrist rest that rolls over and means you:

1. Don't feel like you're digging into your wrists when you try and type
2. Actually have a gap between the base and lid, so you can lift the display easily

Thanks, HP, for returning to 2007. I'm really glad you have it out for the tendons in my wrist.

Makes me feel *appreciated* as a customer.

Especially because the damn wrist rest is so shallow that in a normal typing position (so not scrunching up my fingers like a wicked witch or something) I end up with the pressure point of my wrist *right on that sharp edge*.

Just.

...

Like...

...

Round the edge off? Make the display a little taller, maybe 16:10?

Give yourself that little bit of extra vertical space to play with? That little bit of extra reading space?

That little bit of extra wrist rest?

It would have *really* helped.

Especially for the trackpad.

...

Oh, dear, the trackpad.

It's... well, it's a *trackpad*.

And a really short one at that.

And I've used the Surface Go now.

**And** the Surface Go has a really nice trackpad, despite it being terrible at registering clicks and designed for a 10" form factor.

You see, the Surface Go's keyboard attachment is designed to be *flush* with the table.

It literally gives you a *free wrist rest using the table you're at*. It's brilliant.

The trackpad on the Envy x360 is... not.

It suffers from the shallow wrist rest, because honestly it is just a little too small.

It suffers from the sharp edges that make it a little uncomfortable when you shift your hand to use.

It suffers from this really weird behaviour where you tap, yet it thinks you were dragging.

It's just... kind of a sad little component that clearly got the short end of the design stick.

Especially because there's something it's *really* awesome at.

![](/assets/laptop/IMG_20200815_162529.jpg)

You can use it vertically.

It's kinda awesome.

But again, shows where a slightly taller trackpad would have helped just make it that *little bit better*.

Now, perhaps you don't quite get why I'm enthused about using it vertically.

Well, if you're like me, then you like to lay back on a couch at times.

And using a laptop like that is just *really awkward*.

This way, you look down, and you can use the keyboard *and* see the screen without feeling like a drunk pianist. It's like the onscreen keyboard for a tablet, only *not shit*.

It also means you don't have to tilt your head as much because the screen is being comfortably held up a little higher.

What can I say?

If you're like me, you'd already understand this.

If you're not, well, I guess it'd be best if I moved on to the next point already.

Which is, "what happens if you keep moving the keyboard around the display?"

Well, funny you should ask...

![](/assets/laptop/IMG_20200815_162556.jpg)

*As it turns out*, HP named this laptop the "Envy x360" *not because* they thought it was 360 times better than the normal Envy, but because those (remarkably strong) hinges let the keyboard go around the body to *just behind* the screen, meaning it has 360 degrees of rotation! But not really, because it can't then go through the screen, so it's more like it's *rounded up* to 360... though that *would* be a pretty awesome party trick if it could go through the screen...

Oh, and you'll want to use it this way because then the bottom-firing speakers "magically" become top-firing speakers! So you'll get "magically" improved audio quality and volume!

Imagine that! Top-firing speakers sounding better!

I'll briefly touch on that: I'd wager that the speakers in a pre-production model were looked at by some intern at Bang & Olufsen or something who signed off on the default EQ, so it shouldn't sound like absolute rubbish. Basically just like every other mid-to-high-end laptop these days.

One thing that I don't take for granted, however, is the *internal* audio. The headphone+microphone jack is kinda insane.

Insane in a good way.

My daily driver headphones are a pair of Sennheiser HD 560S's, which I'm used to running at anywhere between 18% and 36% audio volume, depending on the setup. [Edit: I've switched my daily driver recently to the 560S (which are stellar), fortunately what I wrote still holds true.]

Here I'm running them at 2% to 6%.

And it sounds great.

Like, not actually far behind my monitor or my desktop's motherboard (which both have rather good built-in DACs) kinda great. Normal-people headphones won't have any issues here.

So if you're not a snob, you'll feel right at home — just remember to turn the volume down.

Finally, you can make it close up like a tablet and use it that way.

![](/assets/laptop/IMG_20200815_162553.jpg)

And Window 10's rotation mode doesn't disappoint (unless you have maximised windows, in which case they'll end up reflowing and in browsers etc. that can be quite annoying).

![](/assets/laptop/IMG_20200815_162629.jpg)

> Behold. My stuff. (At least I picked a wallpaper that seems to work well in portrait mode, lucky me.)

Now, a minor gripe: even if you disable autorotate, the keyboard will shut down when you rotate out of normal laptop mode, say by holding the laptop at a slight angle. But again, minor gripe, *oh well*.

And there's a big problem with portrait usage here. When you're holding it like this, you will feel all the weight. Ironically, this is because of the small bezels that look *oh so nice* in landscape.

It's not much, only half a pound more than an LG Gram 13", but because the bezels are so thin you will probably want to be like me and hold it daintily away from the screen and rest it in your palm. So the "gem cut" will be digging into your hands whether you like it or not. *Thanks, HP.*

My Surface Go, with its really thick bezels, is actually really nice to hold because you *just grab it*.

Oh well, it's not like it's actually *that* uncomfortable like this. Actually, because you're clasping *around* the sharp edges they're nowhere near as bad as when they're a wrist rest, and the added thickness from having the keyboard there actually does make it a little easier to balance in hand.

You know, because pressure is about force over area, so increased thickness is *more* comfortable.

Now, as a *tablet for reading*, I think the Surface Go is infinitely superior. Why? Because 10" is easier to use as a tablet than 13". More screen is more dragging, less screen is quicker and easier.

And that's okay, I'm keeping my Surface Go for exactly that reason. It's sublime to read papers or blogs on it as the smaller display means I don't move my eyes constantly when I hold it at a comfortable distance, everything is kept in sight and I can read it like a book without turning pages.

But this then handles the other side of "tablet" usage for me far, *far* better: video.

Whether you're watching YouTube or a film, the larger screen is *much* better.

Ironically, this is despite the lower resolution. The Envy has a 1080p panel, while the Surface Go has a 1800x1200 panel. However, the Go struggles to drive 1080@60Hz video or streams, while the Envy handles them with aplomb. More than aplomb, in fact, since you can enable Freesync on the panel it can help a little with juddering if something GPU intense starts in the background (or you forgot to disable your rather heavy upsampling filters meant for 480p footage, sue me).

Additionally, since I use Chromium, this means that a lot of the rendering is being done by a faster GPU now, which means it usually ends up *feeling* quite a bit quicker compared to the Surface Go.

Now, the GPU does come with a downside, and that downside is power draw. Since it's integrated as part of the SoC it *is* a lot more tame than what you might get out of normal dedicated graphics, but it does draw more than Intel's integrated graphics (but, honestly, while a marvel of low-power engineering, the performance of the Surface Go's integrated GPU is embarrassing). Not enough to make you worry, but also enough to mean you probably shouldn't be using YouTube videos for your music while on the go.

Okay, time to use that hinge again and close the laptop up, so I can show you a couple interesting things with the IO. Though first I'm going to give another gripe:

![](/assets/laptop/IMG_20200815_162652.jpg)

Okay, maybe it doesn't quite jump out at you straight away like the fingerprints do.

But let me show a little more directly.

![](/assets/laptop/IMG_20200815_162703.jpg)

See it yet?

![](/assets/laptop/IMG_20200815_162659.jpg)

That's right! Instead of feet, HP decided to put prism ridges across the full length of the base!

So no matter what, you can feel them digging into your *lap* if you ever put any force onto the *laptop*! Like, when, oh *I don't know*, you use the keyboard!

And despite looking like a flush, soft rubber, they're really not!

You feel them! They're hard and annoying!

Well, it's not *that* big of a deal. But it *is* annoying and hey, if you're still reading this then I've basically got a captive audience I can complain to! [Edit: Sadly, HP attached them to the device with a rather weak adhesive. It'd probably have lasted a couple of years "normally", however I had the *audacity* to use my laptop on my lap, and since I rather liked running it on Quiet mode, this meant that at times it got a little warm, which seemed to weaken the adhesive. Long story short, those rubber strips fell out, so I used a much better adhesive and all seems to be fine. *Sigh.*]

... Okay, if you're still reading this, then I guess I might as well give you the good news.

![](/assets/laptop/IMG_20200815_162711.jpg)

That's right! It's a full-sized USB-A port! And micro (grr) SD! Yes, that's a barrel connector and not a USB-C port, I know, it makes me sad as well, but it charges up pretty quick regardless (oh, since I haven't mentioned yet, the UK SKUs have 3-cell 51Wh Li-ion batteries) so 2 out of 3 isn't so bad.

![](/assets/laptop/IMG_20200815_162717.jpg)

On the other side we see the headphone+microphone combo jack (2.5 mm, obviously), ANOTHER full size USB-A (oh my word I don't need to carry a dongle I don't believe it), and then a USB-C port as well! While it's a shame there's no display ports of any kind, HP are kind enough to provide an actual USB-C to HDMI 2.0 adapter with the included accessories, so there's that.

How does the full-sized USB-A port work?

![](/assets/laptop/IMG_20200815_162730.jpg)

Why it has a cute little jaw! It's not hard to open, and you can just push a USB stick in and it should just slide right in, though you may need to wiggle it around to get it to slot in *just right*.

![](/assets/laptop/IMG_20200815_162841.jpg)

The jaw will open out just enough, and because HP pays attention to *some* details I will note that the annoying ridge-foot does have *just* enough clearance for it to open all the way, though the USB device you stick in is another matter entirely.

![](/assets/laptop/IMG_20200815_162832.jpg)

See? It just works. Though I have no idea how long the hinges in the jaws will last, and it might be something you'd need to clean out every once in a while. But, as far as I am concerned, now nobody has an excuse, so I expect USB-A ports (and USB-C) on everything from now on.

Hmm, looking closely... that lightning bolt symbol... could it be... Thunderbolt on a Ryzen chip?

Well, sadly not. That's just HP being terrible at picking their symbols.

What it actually means is apparently called "HP Sleep and Charge"... normal people know this as "charging your laptop over USB".

Wait...

What?

But it has a barrel plug?

Yes! As it turns out, you can charge the HP Envy x360 over the USB-A port on the barrel plug side or over the USB-C port! You just need a 65W USB cable and charger. Lower Wattage might mean trickle charging the device or, if you're giving less than 15W, just delaying the inevitable!

Well, I'll be!

And let me simplify what the USB ports actually mean for you as well, because apparently the USB Implementers Forum can't be trusted to name things any more. (Naming rights hereby revoked.)

The USB-C port is the star of the show and runs at 10Gbps (that's giga- as in billions and bits as in individual bits, not bytes), so it *can* transfer a full 1 GIGABYTE per SECOND. Of course, this only works if the device and/or cables you plug in are rated for this transfer speed, but at least it's there.

The USB-A ports on this laptop run at 5Gbps, so again if the device you're plugging in supports this transfer speed then you're in luck! And to save you the conversion, that's 625MBps maximum (that's mega- as in millions and Bytes as in 8 bits at once).

And like all things that's the maximum *rated* speed, if you're moving files then it will fluctuate based on the size of the file, the duration of the transfer, the temperature of the USB device (they can get pretty toasty) and the activity of the laptop (the NVMe drive *should* be able to handle it but if all 8 cores are hammering it with reads and writes then performance degradation is to be expected).

Now, for some final gripes at HP, quick-fire round style:

1. HP limited the UK SKUs to only having the 300nit panel for some bizarre reason
2. HP limited the UK SKUs to only having Wi-Fi 5 802.11ac, so no Wi-Fi 6 (let alone 6E)
3. THAT FUNCTION + L FOR BACKSLASH MONSTROSITY; DEVS NEED A DEDICATED `\` KEY! 😡
4. Because of their *cute* privacy cover mechanism apparently they can't fit IR for Windows Hello
5. Bluetooth initially had some trouble connecting to my Sony WH-1000XM3 headphones
6. MicroSD slot is always more awkward than full size SD slot because converting down is hard
7. Webcam is 720p and bad; HP, if your tag line is "Carry on creating" then put in a *good* camera
8. Microphone is "okay", serviceable, but picks up on everything from keyboard to touchpad clicks
9. Only 2 levels of backlight before "off", all are too bright, especially for low-light/at-night usage
10. Little bumps above Escape and Delete are annoying, and I keep pressing them on accident
11. Bloatware still present, basically all useless or redundant in Windows 10, UWP is ugly as ever
12. Fingerprint reader not backlit/ring lit, looks out of place because of it
13. Battery could be bigger, I don't mind a little extra weight if I got 60-65Wh
14. Gem-cut is the worst part of the design (except the keyboard, no forgiving that), round it off
15. Please just go 16:10, at 13" it's already too big for portrait mode with a 1080p panel
16. MORE AND BETTER UK SKUs, SERIOUSLY, WHAT'S WITH THE UNDER-SPECCING?!?!

Well, there we have it. I hope that wasn't too much of a drag to read.

I do truly think this is a very nice laptop, and I'm amazed at how far Zen 2 has come.

I just hope HP can address some of my problems for future revisions, such that people do not have to suffer like I will. A slow death by a thousand tiny gripes.

Now, I'm off to do something else, this took far too long to write.

[Edit 2022-09-05: After two years of ownership, I am still pleased with this and continue to daily drive it. The issues are still issues, and of those the biggest has remained the battery. I just need more capacity, especially given how much video and video conferencing I've been expected to watch and take part in over these last two years. Still, solid, so when it eventually dies I may more easily consider a direct refresh.]
