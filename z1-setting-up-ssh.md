# Z-1. Setting up SSH

This is an optional step, but it has two significant benefits.

1. It is more secure than the default of using a password (SSH stands for "secure shell"!).
2. It is actually way easier to use than the default once you have it set up, because you don't have to enter your username and password each time you interact with the remote.

(Note: You can find more complete info on SSH with GitHub [here](https://help.github.com/articles/connecting-to-github-with-ssh/). That is where most of this
info is coming from.)

## Generate an SSH key

An **SSH Key** is a large random number used for encrypting an decrypting messages. It also sort of serves as your identity on the Internet, in that services
will use it to verify whether a message actually came from you.

First, make sure you don't already have a key. In your terminal, enter:

```sh
ls -al ~/.ssh
```

If it comes up empty, then you're good to create a new key. If there is something there, e.g., `id_rsa` and `id_rsa.pub`, then you already have a key, and you
can skip to the next step.

If you're creating a key, enter the following into your terminal: (replace the email address with your actual email address)

```sh
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

That means, "Hey program called ssh-keygen, make a key using the standard (RSA) encryption type, make it 4096 bytes, and use my email address as a way to make
it personal."

It will ask you a few more questions. You can probably just hit enter through them, because the defaults are typically fine, unless you have a particular
preference to do otherwise.

Importantly, this generated two files. One is called `id_rsa`, and the other is called `id_rsa.pub`. The `.pub` file is called a **public key.** It is what you
give to whoever/whatever is going to be decrypting your messages. The one without an extension is called a **private key.** You *do not* want to give that key
to anyone or any website. It is the one you use to encrypt your messages, and then they can only be decrypted with your corresponding public key.

Once the key is generated, enter the following lines:

```sh
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_rsa
```

## Adding the key to GitHub

Now you need to tell GitHub what your public key is so that it can verify your identity when you send it commits.

First you need to copy your public key. In your terminal, try:

```sh
xclip -sel clip < ~/.ssh/id_rsa.pub
```

If that returns an error that xclip is not installed, you can just use `cat`:

```sh
cat ~/.ssh/id_rsa.pub
```

to print it to the screen, and then copy it normally (highlight, right-click, and select copy, or Ctrl/Cmd+Shift+C)

Then go to GitHub, and on the top right, click on the arrow next to your icon, and then click "Settings."

On the left bar, click "SSH and GPG keys."

On the top-ish right (green button), click "New SSH key."

Add a title that will help you identify which computer it's from.

And then paste the key in the box, and hit "Add SSH key."

Then run a test connection to GitHub from your terminal:

```sh
ssh -T git@github.com
```

It should print out, "Hi [your username]! You've successfully authenticated, but GitHub does not provide shell access."

## Using SSH with existing GitHub repositories

Now that you have SSH set up, you should use instead of HTTPS (the default) for your connections to GitHub. That means that if you already have repositories
with remotes set up, you'll need to change the URLs of the remotes to use SSH. If you forget, you'll be reminded that it's still using HTTPS when it asks you
for a username and password. **If you're using SSH, GitHub will not ask for a username and password.**

A typical HTTPS URL will look like `https://github.com/USER/REPOSITORY.git`. An SSH URL will look like `git@github.com:USER/REPOSITORY.git`. So the only two
things that change are 1) the prefix (from `https://` to `git@`), and 2) the "/" after "github.com" becomes a ":".

To see the URL for the "origin" remote, enter:

```sh
git remote get-url origin
```

To update it, enter:

```sh
git remote set-url origin git@github.com:USER/REPOSITORY.git
```

(but replace USER and REPOSITORY with your username and the repository name).

## Using SSH with new GitHub repositories

From now on, when choosing a URL clone a repository or to add origin as a remote, choose the SSH one. If SSH is enabled on your GitHub account, it should show
your the SSH URL by default.

Everything else works just like before, but with the SSH URL instead of an HTTPS one.

To clone a repository:

```sh
git clone git@github.com:USER/REPOSITORY.git
```

And to add a remote:

```sh
git remote add origin git@github.com:USER/REPOSITORY.git
```
