---
layout:  post_content
title:  "ssh-keygen"
date:   2018-02-22 13:16:01 -0600
comments: true
excerpt_separator: <!---excerpt--->
---

Generating a new SSH key

<div class="codeblok">{% highlight shell linenos %}
ssh-keygen -t rsa -b 4096 [email address]
{% endhighlight %}</div>
<!---excerpt--->
This creates a new ssh key, using the provided email as a label.

Generating public/private rsa key pair.

When you’re prompted to “Enter a file in which to save the key,” press Enter. This accepts the default file location.

<div class="codeblok">{% highlight shell linenos %}
Enter a file in which to save the key (/home/you/.ssh/id_rsa): [Press enter]
{% endhighlight %}</div>

At the prompt, type a secure passphrase. For more information, see “Working with SSH key passphrases”.

<div class="codeblok">{% highlight shell linenos %}
Enter passphrase (empty for no passphrase): [Type a passphrase]
Enter same passphrase again: [Type passphrase again]
{% endhighlight %}</div>

This will have created a key named id_rsa and id_rsa.pub wherever you specified above.

Now you must copy the public part to your server, or if your already on your server then simply to ~/.ssh/authorized_keys

If you’re not on your server you can do this by entering:

<div class="codeblok">{% highlight shell linenos %}
sudo scp -P XXX ~/.ssh/id_rsa.pub user@machine.domain.com:/home/user/Documents/id_rsa.pub
{% endhighlight %}</div>

Then on your server simply enter this:

<div class="codeblok">{% highlight shell linenos %}
sudo mv ~/Documents/id_rsa.pub ~/.ssh/authorized_keys
{% endhighlight %}</div>

Then on your client simply using the matching id_rsa or id_rsa.ppk file and your good!

Now this may seem simple, but I’ve had problems with permissions for these files for hours once at the beginning. A little tip – authorized_keys should be chmod 600 and .ssh chmod 700. Therefore only the owning user can read and write them. Sshd seems to be picky about this..

<br>
{% man 1 ssh-keygen Ubuntu %}<br>
{% man 1 ssh Ubuntu %}
<br>
