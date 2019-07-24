---
layout: post
title: Find all values for default write using default read on macOS
---
I've been looking at setting myself up with a [dotfiles](https://dotfiles.github.io) repository (very late to the game!)
and in the process I've been reading through the usual set of recommended starter repos etc and was interested in some
of the macOS specific options various people have included using custom `default writes` such as in [Mathias Bynens' .macos](https://github.com/mathiasbynens/dotfiles/blob/master/.macos)
file.

I then wondered if there was as single go-to list of all possible settings (although unsure of how long that would be
exactly) and found this [SO question](https://apple.stackexchange.com/questions/251356/how-to-get-a-list-of-available-defaults-write-terminal-commands-for-os-x-el-ca?newreg=657aae87b1374367bc8d626d26f997d4)
asking the same.

Unfortunately it's been closed as too broad (not exactly sure why as seems like a perfectly valid question to me, but
hey that's SO sometimes for you!), although there is a nugget in the comments about using `defaults read`. If you try
running this, it could be a bit overwhelming as it clocks in at over 50,000 lines on my system!

Another clue in that post however pointed to the fact that the actual settings are stored under `~/Library/Preferences`
and a quick `ls` in here will show various `.plist` files. If you try and read these, you'll just get gobbledygook as
they're binary, but it occurred to me you could just pass a namespace as a parameter to `defaults read` and sure enough
it works e.g. `defaults read com.apple.finder.plist` will give you a much more manageable (albeit 2,000 lines) of
settings just for finder. Of course you're now free to look at each of these files and try and extract any settings you
may want to transfer to your dotfiles project and run consistently on any system in the future.


