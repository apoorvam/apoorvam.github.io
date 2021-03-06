---
layout: post
title:  "Import secret GPG keys from one machine to another"
date:   2016-07-14 15:04:49
comments: false
categories: gpg import transfer
---

If you have GPG keys generated in one machine say `machine1` and now you want to transfer it to another machine say `machine2` along with secret keys, here is how you can do.

In `machine1`, export the public and private keys as follows.

{% highlight sh %}
gpg --export ${ID} > public.key
gpg --export-secret-key ${ID} > private.key
{% endhighlight %}

Copy these public and private keys to `machine2`. In case of Unix, you can use SCP (the `scp` command) to securely copy files and directories between remote hosts.

In `machine2`, go to the directory where you copied the keys to and run the following commands.

{% highlight sh %}
gpg --import public.key
gpg --allow-secret-key-import --import private.key
{% endhighlight %}

Here, the flag `--allow-secret-key-import` gives the gpg permission to import private keys and flag `--import` will actually import the key.

Now you can use `gpg --list-keys` to list all the GPG keys.