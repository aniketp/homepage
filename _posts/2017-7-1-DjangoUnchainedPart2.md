---
layout: post
title: Dynamic Django (Part-2)
author: Aniket Pandey
---

Continuing where I left off previously..
Creating the library portal was a boon for us. It had only been three weeks(less than half the time) since the camp started, 
we had completed our backend functionality.

This headstart gave us enough time to actually think about the features that we would be adding in to the portal, we often had
long discussion sessions with each other and also with our mentors. While Pratham would clear all our Django related doubts,
Yash had a decent knowledge of what was to be included in the portal. 

### The dynamic heirarchy

This is the flashing point of our project. Initially when Kunal was explaining us about the specifics of the project, he mentioned 
something called infinite level of heirarchy. What it means is that there should not be any limit on the number of posts 
that are possible. A club should be able to have as many posts as required, either 2 or 3 or even 50. 
 
Although it seems a daunting task to accomplish, it did not cause much problems in the end. Thanks to Ashish, we were able to 
figure out a way to do so. What we did was that we linked a _Post_ model to itself and named it _parent_. 
```
class Post(model.Models):
    post_name = models.CharField(max_length=500, null=True)
    club = models.ForeignKey(Club, on_delete=models.CASCADE, null=True, blank=True)
    parent = model.ForeignKey(self, null=True, blank=True)
    post_holders = models.ManyToManyField(User, related_name='posts', blank=True)
```

These are four of many columns in the Post table. The third line is what turned the table for us. Although it may seem too
trivial, we did not know abot self linking at that time. We had to research a lot to be able to get to something like this.

### The dynamic forms

This is another highlight of the portal. Mostly written by Ashish. It allowed us to create dynamic forms, that is, while
releasing nominations, the admins can create forms which the applicants have to fill. The filled forms can then be evaluated
by the interview panel, regarding which they can add few comments of their own. 

This is how the process goes underway, the only difference (and benefit of switching over to the new portal) is that everything 
could be done at a single place. No need to create a separate Google form and record comment in your own laptop and then finally 
create a list of selected applicants. All of it is taken care of in the portal. 
 
### The dynamic approval system

Most of the stuff that happens in gymkhana needs an approval from higher authority. Mostly by the Gen-Secs or the Chairperson.
While creating a Post or a Nomination You need a final approval from the concerned authority.

This was another challenge for us, as to accomplish it, we needed to create a ladder like functionality so that an approval 
can climb up the ranks and after getting a heads-up from the admin, it would be in effect. 

It was another genious effort from our side to get around this problem. We created a separate field in _Post_ and _Nomination_
models:
```
class Post(model.Models):
    ...
    post_approvals = models.ManyToManyField('self', related_name='approvals', symmetrical=False, blank=True)
    
class Nomination(model.Models):
    ...
    result_approvals = models.ManyToManyField(Post, related_name='result_approvals', symmetrical=False, blank=True)
    nomi_approvals = models.ManyToManyField(Post, related_name='nomi_approvals', symmetrical=False, blank=True)
```

You would observe there are three different approval fields `post_approvals`, `result_approvals`, `nomi_approvals`. These 
columns contain the list of all the Posts, above the post for which the nomination was released. Once it passes through a 
 certain level, the very next level gets added to the approvals list. So our Nomination knows where to go next for approval.
 This continues till it reaches the highest authority, on whose approval, the nomination is released for public. 
 
Same can be said for Posts, although it is highly unlikely that any additional posts would be created. But, to make it more dynamic,
we allowed separate posts to be created, just in case..