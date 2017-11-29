+++
title = "Use IFTTT Maker Channel to Trigger Events in a Django App"
date = "2016-04-08 7:15:00"
categories = ["Programming"]
tags = [
    "django",
    "python",
    "ifttt",
    "maker",
]
+++

A couple months ago I decided I needed to be better about telling my wonderful wife how much I loved her on a daily basis. Being the nerd that I am I decided to tackle this using [IFTTT][1] and a custom web app. For this project I went with [Django][2] to build my app out. I'd never used it before so I wanted a chance to play with it.

## The idea

The idea is pretty simple. IFTTT will, using their [Maker Channel][3], send a request to any endpoint that you want with a custom payload. I figured I could have that run daily to hit my app, which would then pull a reason that I love my wife from the database and send it to her.

In my case, I decided to utilize IFTTT to also **send** the love notes as well. The Maker Channel can not only send requests, but it can receive them as well. So I would pull a reason from the database, send that reason **back** to IFTTT which would then email it to my wife for me using my own Gmail account. Believe it or not, this was easier than trying to hook up my Gmail account to send the emails myself.

## Execution

### Django App

My Django app is **really** simple. I have two routes, my `admin` route and a single `index` route. I'm using the default Django admin console to add love notes to the database. The index route will handle requests from IFTTT to trigger sending a love note. It also serves up some basic HTML in case anyone accidentally finds this application in the wild. IFTTT passes along a security token so that I know when a request should trigger sending a love note or not.

Before I dive into explaining the code, you can check out the [Github Repo][5] for yourself. Feel free to copy all or parts of it for your own use!

#### Security

You're not going to want just anyone to be able to trigger sending love notes from your app. You'll need some security in place. Thankfully this is pretty simple using `Environment Variables` in your Django app settings. The relevant part of my `settings.py` looks like this:

```python
SECRET_KEY = os.environ.get('SECRET_KEY') or "youhavemyheart"
IFTTT_KEY = os.environ.get('IFTTT_KEY') or "youhavemyheart"
```

I'm using `os.environ.get` to pull the values from my `Environment Variables`. To learn more about setting this up when you Deploy your app check out this guide check out these two links:

1. [Using Supervisord][6]
2. [Using uwsgi][7]

The `IFTTT_KEY` might be a little confusing, but when you actually connect the [Maker Channel][3] to your IFTTT account you'll see a part that says "Your key is:". You just need to use that secrete key in your own `Environment Variables`. Please be sure not to put this value (or your `SECRETE_KEY`) in your actual code. Doing so is a huge security risk if you plan to push your code to a remote respository or share it in any way.

#### Index Route

Here's what the `index` route looks like (if not a little simplified):

```python
from django.http import HttpResponse
from .models import Reason
import requests, os
from LoveDb.settings import SECRET_KEY, IFTTT_KEY

def index(request):
    response = """
    	A brief message in case anyone arrives at this page by mistake.
    """

    their_key = request.GET.get('key', '')
    my_key = SECRET_KEY

    if(their_key == my_key):
        reasons = Reason.objects.filter(been_used=False).order_by('-created_date')[:1]

        if(len(reasons) > 0):
            reason = reasons[0]

            love_note = {}
            love_note['value1'] = reason.reason_text

            # Send via If This Then That
            requests.post("https://maker.ifttt.com/trigger/send_love_note/with/key/{0}".format(IFTTT_KEY), data=love_note)

            # Update reason so that we don't use the same one twice (wouldn't that be embarrassing!)
            reason.been_used = True
            reason.save()

    return HttpResponse(response)
```

#### Love note (or `Reason`) model

Of course, I need to actually STORE the love notes somewhere. I created a `Reason` model to do this.

```python
from django.db import models


class Reason(models.Model):
    reason_text = models.CharField(max_length=200)
    been_used = models.BooleanField()
    created_date = models.DateTimeField('date created')

    def __str__(self):
        return self.reason_text
```

I also need to be able to add things to the database using this model, enter Django admin. The Django admin was actually one of the biggest reasons I used Django for this project. I didn't have time to write user auth or CRUD interfaces. I just needed something simple that did the job. And simple it is:

```python
from django.contrib import admin

from .models import Reason

class ReasonAdmin(admin.ModelAdmin):
    list_display = ('reason_text', 'created_date', 'been_used')
    list_filter = ('been_used', 'created_date')

admin.site.register(Reason, ReasonAdmin)
```

### IFTTT

The maker channel is pretty easy to use. If you're not familiar with IFTTT, then you should know that IFTTT has two types of things it can do / handle:

1. Triggers: things that do things based on certain events or at certain times
2. Actions: Things that are triggered by other events.

So, for my purposes I'm going to use the [Date & Time][4] Channel to _trigger_ an _action_ on the Maker Channel. The action on the Maker Channel will make a request to my Django app to trigger sending a love note.

Sending of the love note will _also_ be done by IFTTT. Once my app gets a love note and is ready to send it I'll pass it back to IFTTT, again using the Maker Channel to consume a request (this is a _trigger_).

#### Trigger Sending of a Love Note

This recipe is really simple. Just pick a time and enter the URL of your Django app that you're using to recieve the trigger. Don't forget to enter the secret key you set up for your app in a `GET` parameter on the URL. Your URL should look something like this:

`http://yourawesomelovedb.com/?key=YOUR_SECRET_KEY_HERE`

And here's the recipe for you to use right here!

<a href="https://ifttt.com/view_embed_recipe/406032-trigger-sending-a-love-note-daily" target = "_blank" class="embed_recipe embed_recipe-l_33" id= "embed_recipe-406032"><img src= 'https://ifttt.com/recipe_embed_img/406032' alt="IFTTT Recipe: Trigger Sending a Love Note Daily connects date-time to maker" width="370px" style="max-width:100%"/></a><script async type="text/javascript" src= "//ifttt.com/assets/embed_recipe.js"></script>

#### Send the actual Love Note

Sending the actual love note is really simple. You just hook the Maker Channel up to gmail and away you go! I'm using the `Value1` part of the Maker Channel trigger for the body of the love note, which you saw in the `index` route of the app. As long as you copy that index route this recipe should be as simple as entering the name of the Love Note event (I named mine `send_love_note` which you saw in the `index` route) and the Email address of the person you're sending the love note to.

<a href="https://ifttt.com/view_embed_recipe/406029-send-a-love-note" target = "_blank" class="embed_recipe embed_recipe-l_16" id= "embed_recipe-406029"><img src= 'https://ifttt.com/recipe_embed_img/406029' alt="IFTTT Recipe: Send a Love Note connects maker to gmail" width="370px" style="max-width:100%"/></a><script async type="text/javascript" src= "//ifttt.com/assets/embed_recipe.js"></script>

## Conclusion

Now, I'm sure that this guide is missing steps, and is probably wrong in some places. But I hope that it's valuable as a jumping off point for anyone who wants to do something similar. Let me know in the comments what you think, or what you used this guide to make!

<!-- Links -->
[1]: https://ifttt.com "If This Then That"
[2]: https://djangoproject.org "Django Project"
[3]: https://ifttt.com/maker "IFTTT: Maker Channel"
[4]: https://ifttt.com/date_and_time "IFTTT: Date & Time Channel"
[5]: https://github.com/CrowderSoup/LoveDB "Github Repo for the LoveDb"
[6]: http://supervisord.org/subprocess.html#subprocess-environment "Subprocess Env"
[7]: https://coderwall.com/p/93jakg/multiple-env-vars-with-uwsgi "Multiple Env Vars with uwsgi"
