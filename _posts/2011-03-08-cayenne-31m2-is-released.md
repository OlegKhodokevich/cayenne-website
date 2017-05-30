---
layout: post
title:  Cayenne 3.1M2 is Released
date:   2011-3-8
---

We keep improving Cayenne 3.1 with the new M2 milestone release. If you've already experimented with 3.1, M2 is a must-have upgrade - it fixes a number of bugs that affected runtime stability (CAY-1515, CAY-1519). If you haven't, maybe it is time to try it out? ;) Usual disclaimer applies about M2 being an early alpha and the new APIs being subject to change. In addition to the numerous bugfixes in the runtime and the Modeler, the new release introduces a set of brand new powerful tools for object lifecycle management. We'll briefly describe them here. Please check Guide to 3.1 Features for more details.

* Cayenne now allows to declare listener methods with annotations. Configuring listener methods in the Modeler (or via API for that matter) was arguably the most tedious mapping task in Cayenne. What's even worse, if you reuse your model in more than one app, you may not want the listeners to be shared, so you don't want them to be in the model at all. M2 solves that by letting you to annotate the listener class, and registering a listener object where you need it with a single method call. A listener object can of course have multiple annotated callback methods:

        MyListener listener = new MyListener();
        runtime.getChannel().getEntityResolver().getCallbackRegistry().addListener(listener);

While JPA users may think that lifecycle annotations is old news, Cayenne goes a bit further than JPA here. Cayenne annotations let you attach a listener not just to specific entities, but also to entities whose names are not known to the listener upfront. A listener annotation may reference an arbitrary user-defined annotation which is then placed on entity classes. All of this completely changes how you manage your listeners. It becomes simple, clear and flexible.

* Another cool lifecycle management tool is DataChannelFilter. A chain of filters can be configured by the user to intercept and react to the data traffic (selects, commits) between DataContext and DataDomain. This was sort of possible before by decorating a DataChannel, however the new approach is much less invasive, and more importantly, the filter object can also have annotated listener methods that are aware of the ongoing select or commit operation. That's what ultimately makes it usable in real-life situations. CacheInvalidationFilter in cayenne-lifeycle module (cayenne-lifecycle is described below) is a good example of how a filter collects some information about an ongoing persistence operation in a ThreadLocal object, and then processes aggregated information at the end of this operation.

* We are taking advantage of the above feature by providing a cayenne-lifecycle extensions module that implements a few common lifecycle management scenarios - object audit, automated cache group invalidation, and handling a new kind of "to-any" relationship (we tentatively called that one a UuidRelationship). You may use cayenne-lifecycle goodies as is, extend them, or simply refer to it as an example of what is possible with the new lifecycle tools. There's still lots of experimentation going on here, so its API is likely to change.

Finally, 3.1M2 [download link](/download.html).