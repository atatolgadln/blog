---
title: "Discord Experiments"
date: "2022-04-27"
---

> ⚠️ It's breaking TOS so be carefully

If you want to try things that discord does that are not yet published you need to do a few things. In this post we'll show how to unblock the "Experiment" tab and how to download the development version of Discord (no canary but you can use canary).

# Download development version of Discord
When we want to try the latest unreleased stuff, we need a different client than Canary. These things come to canary later.
You need to download Discord Development. Just open this link:

- https://discordapp.com/api/download/development?platform=win (Windows)

- https://discordapp.com/api/download/development?platform=linux&format=deb (Linux, deb)

- https://discordapp.com/api/download/development?platform=linux&format=tar.gz (Linux, tar.gz)

- https://discordapp.com/api/download/development?platform=osx (Mac)

# Open console, use script
If we already have Discord Development downloaded, all we need to do is open the console in the client using the shortcut CTRL + SHIFT + I and then paste this code into the console:
```JavaScript
webpackChunkdiscord_app.push([["wp_isdev_patch"], {}, r => cache=Object.values(r.c)]);
var UserStore = cache.find(m => m?.exports?.default?.getCurrentUser).exports.default;
var actions = Object.values(UserStore._dispatcher._actionHandlers._dependencyGraph.nodes);
var user = UserStore.getCurrentUser();
actions.find(n => n.name === "ExperimentStore").actionHandler.CONNECTION_OPEN({
	type: "CONNECTION_OPEN", user: {flags: user.flags |= 1}, experiments: [],
});
actions.find(n => n.name === "DeveloperExperimentStore").actionHandler.CONNECTION_OPEN();
webpackChunkdiscord_app.pop(); user.flags &= ~1; "done";
```
This code will set the isDeveloper property to true.

# Test experiments
Finally, all we have to do is go into the settings and at the very bottom we'll see the Experiments tab. We click on that, and we'll see experiments. You always have a select menu where you can choose what type you want.
