# Getting started

Typst is an open-source project that can be built into a pretty small binary, that is very easy to install or even use in Web. Typst is managed and built by a company, a company, the main product of which is Typst editing Web App.

So there are two possibilities for working with Typst: use online Web App or install Typst locally and work with it from your favorite editor. I will briefly cover these two ways with their pros and cons in this chapter.

## WebApp

Starting is pretty simple: sign on [typst.app](https://typst.app) and create a new document. Then... Just start typing, and the document with your text will appear in the preview Panel.

I highly recommend starting from scratch at first to try things. When you get some better understanding on Typst, you can continue with _templates_, instructions to style your document ready-to-use. But even then, sometimes it is just easier to make all you need exactly as you need from scratch. Typst makes it easy.

**Pros**:

- Very easy to start
- Perfect for collaboration.
- _Features:_ Typst Team has put lots of effort into the app, so it has a lot of pretty good features (like smart dictionary check or Vim keybindings for pros).
- _Working Offline_: Once the page is loaded, you can go offline. Compiling document is done on your computer, so you don't need internet connection to make it. And all changes will be saved locally. 
- Easy to work with same projects across devices.
- Comes with even more cool features at their paid plan, Typst Pro: like comments for collaboration and Github sync. 
  It's also a pretty good opportunity to support the project (though there are other ways to support them, like Github Sponsors, contributing and spreading the word about Typst `:)`).

**Cons**:

- Still requires internet
- Your data is stored online, your development (however, you can make backups and the app crashes very rarely)
- The App lacks some features that are present in local editors and Tinymist LSP.
- With local compiler, you can do pretty wild automations, like making automatic report generators.


## Local development

### Tinymist

> Don't use Typst LSP, that's a very outdated thing.

Tinymist is a community-developed LSP [^1] that probably has even more features than Web App (well, that may change in some time, and I'm not known for keeping this book very up-to-date). These include things like going-to-defenition, refactoring, formatting,, opening packages the errors are comming from and many-many others. It's not "official", but it doesn't make it any worse. It is definitely worth trying.

Works with pretty much any editor supporting LSP. For VS Cod(e,ium), Neovim, Emacs, Sublime Text, Helix and Zed there are also useful frontends available.

So, to use Typst locally, it's probably enough to open your favourite editor, install Tinymist extension and get a full Typst experience with live preview and many other nice things.

> Tinymist uses Typst as a library, so it comes with it's own inner Typst version. Sometimes, for example, if your VS Code version is too old, it can't install newer version, and you end up with old Typst version without knowing it.

> Oh, yep, Tinymist can export documents in any needed format, by the way. You can also set up it to do it automatically on save, too.

> And it's actually possible to just use `tinymist preview document.typ` from terminal, if it's a properly installed tool (that would open a browser preview).

**Pros:**

- _Features:_ probably _the largest set_ available for Typst.
- Best for programmers or experienced users.
- It's just a LSP, all other things you need come from your editor, system and so on. It's easy to work with Github, easy to integrate it in whatever you want.

**Cons:**

- It's probably a bit harder than just launching WebApp.
- Collaborating that way is much harder. It requires using Github or setting up your editor.
- Worse portability (you have to sync your files).
- There are tiny chances that the development will be dropped in future.

### CLI

Typst also comes with it's own CLI (command-line-tool). This way, it is enough to install on your system and then launch from terminal `typst c your_file.typ` (or `compile` instead of `c`) to get a PDF, compiled from your `your_file.typ` document.

> Installation notes:
> - Windows users: just download the exe from Github Releases and unpack it somewhere in your PATH
> - Unix users: https://github.com/typst/typst?tab=readme-ov-file#installation.
>   Note: Typst version sometimes significantly lags at package managers (and it's not Typst' fault).

This way, you can open your favorite text editor, like Notepad (or Vim without any plugins), write Typst document there, then compiling it and looking at the result.

CLI also supports _watching_ file: `typst w your_file.typ` (or `watch` instead of `w`). That way, Typst will recompile it each time it is changed (and saved).

That way, however, I recommend having a _live preview PDF viewer_, that would update the viewed PDF as it is changed with need for reload.

These include:

- SumatraPDF (works on Windows)
- Zathura and Sioyek (Linux)
- MuPDF (must be combined with `entr` on Unix)
- (some others I've forgotten, feel free to make an Issue / PR)

(note that it is not perfect, there probably would be some blinking, but it's much better than having to reload)

**Pros:**
- Perfect for "I need to quickly compile this file". You can use it along with Tinymist, using Tinymist for preview and editing, and CLI for the fast and precise exporting.
- Perfect for complex automations and using it from other apps.
- Can self-update for required version with one command (if installed not from package manager)

**Cons:**
- Harder to use
- Doesn't provide editor features

## Let's go

I hope you have managed to get something working, so let's go diving into Typst!

[^1]: A language-server protocol, a thing that provides cool things like autocompletion or refactoring features for most editors.