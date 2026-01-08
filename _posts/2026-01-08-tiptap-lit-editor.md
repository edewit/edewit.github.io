---
layout: post
title: Bridging the Gap: How We Made Quarkus Roq Feel Like a Modern CMS
author: Erik Jan de Wit
tags:
- web
- development
---

# Bridging the Gap: How We Made Quarkus Roq Feel Like a Modern CMS

Every great tool has an origin story, and the **[tiptap-lit-editor](https://github.com/edewit/tiptap-lit-editor)** is no exception.
It wasn’t born out of a desire to create "just another editor," but rather from a specific need to bridge two worlds: the speed of static sites and the flexibility of a modern CMS.

### The Spark: Roq and the Quest for the Perfect CMS

The story starts with **[Quarkus Roq](https://iamroq.com/)**.
If you aren’t familiar, Roq is a "supersonic" static site generator (SSG) built for the Quarkus ecosystem.
It allows you to build blogs and websites with the same ease as Jekyll or Hugo, but with the full power of Quarkus under the hood.

However, we hit a classic dilemma.
Static sites are amazing for performance and SEO, but they often lack the "live" feel of a CMS.
You usually have to open a code editor, tweak a Markdown file, and push to GitHub just to fix a typo.
We wanted to make Quarkus Roq **both static and dynamic**—a system where you can enjoy the stability of a static site but have the power to edit content on the fly, just like a high-end CMS.

To do that, we needed an editor that was as flexible as the web itself.

### Enter Tiptap and Lit

We chose **Tiptap** because it’s the gold standard for headless rich-text editing.
But we didn't want to lock ourself into a specific framework like React or Vue.
We wanted something universal.

By building the editor with **Lit**, we’ve turned it into a native **Web Component**.
This is the "secret sauce" of the project.
Because it’s a standard custom element, you don't have to worry about framework silos.
Looking back at it made us realize that this could be something that would be good for others as well, so we desided to create a reusable component from it.

### Why You’ll Love Using It

The beauty of this editor is that it’s "plug and play" in the truest sense.

1. **Framework Agnostic:** Whether you are using React, Angular, Svelte, or even just a plain HTML file with no framework at all, you can drop in the `<tiptap-editor>` tag and it just works.
2. **Slash Commands & Blocks Bubble menu and Drag and Drop:** Just like Notion, you can type `/` to pull up a menu of blocks.
   It makes structured content creation feel like a breeze rather than a chore.
3. **Lightweight & Fast:** Thanks to Lit’s tiny footprint, the editor is incredibly fast, keeping your bundle sizes small and your lighthouse scores high.

### Bridging the Gap

By integrating this editor into the Roq ecosystem, we’ve effectively turned a static site generator into a dynamic content powerhouse.
You can edit your posts in a beautiful UI, and when you're done, Roq handles the "static" magic.

It’s about giving developers the best of both worlds: the reliability of a static site and the seamless user experience of a dynamic CMS.

Ready to give it a spin?
Head over to the **[tiptap-lit-editor GitHub repo](https://github.com/edewit/tiptap-lit-editor)** and see how easy it is to add a world-class editing experience to your next project!

---

