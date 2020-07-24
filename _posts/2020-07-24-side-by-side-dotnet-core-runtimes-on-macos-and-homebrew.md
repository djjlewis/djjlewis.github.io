---
layout: post
title: Side-by-side .NET Core SDK and ASP.NET Core runtime on macOS and Homebrew with dotnet-install scripts
---
# TL;DR
Download the `dotnet-install script` from the [.NET Core Downloads](https://dotnet.microsoft.com/download) site and run:

`$ ./dotnet-install.sh --channel 2.2 --install-dir /usr/local/share/dotnet --runtime aspnetcore`

Substituting your required options for version, install directory and adding runtime if you don't need the SDK.

---
After recently repaving and clean installing macOS Catalina on my MacBook Pro, I made a promise to myself that where
humanly possible I will only install new tools, utilities and apps with Homebrew (as it happens using Brewfile "bundles"
that I am keeping up to date in my dotfiles repo).

As a .NET developer, I will always want the latest version of the .NET SDK and runtime which is easily done via a
quick call to `$ brew install dotnet-sdk`. However, unlike some packages, older versions are not available so will
always intall the latest, currently 3.1.

For reasons I do not yet fully understand, I am unable to debug ASP.NET Core 2.2 apps with the 3.1 SDK, presumably
because it _requires_ one of the ASP.NET 2.2 runtimes to be installed (App or All).

Not wanting to b0rk my donet core Homebrew installation of dotnet, I had a look around to see if it was possible to
install a different package and sure enough I found a [github project](https://github.com/isen-ng/homebrew-dotnet-sdk-versions) that supplies casks for alternative versions of
the SDKs, however I didn't really want or need the full SDK, just the 2.2 ASP.NET Core runtime.

One option would be to just download and install the 2.2 runtime .pkg for macOS from the [.NET Core download
page](https://dotnet.microsoft.com/download/dotnet-core/2.2), but sticking to my philosophy of keeping things scriptable
and repeatable, I noticed an option to download the 'dotnet-install scripts'. 

Downloading and running `$ ./dotnet-install-sh --help` (remember to `chmod u+x` the file) shows a wealth of options
provided by this monster script.

Of interest to me were the `--channel`, `--install-dir` and `--runtime` options as my goal was to install 2.2
specifically, in the same installation directory that homebrew puts dotnet, and only installing the ASP.NET Core runtime.

The full command to achieve this was `$ sudo ./dotnet-install.sh --channel 2.2 --install-dir /usr/local/share/dotnet --runtime aspnetcore`.

You can also helpfully add the `--dry-run` and `--verbose` options to get an idea of what the script will do with affecting
anything.

For me `sudo` was also needed as my normal account did not have all the required permissions for the script to complete.
