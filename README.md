# REQUIRED RESPONSES
Name: Matthew Sporman

Date: October 23rd, 2025

Hours spent: 5 hours

Hyper-link: https://drink-menu-24g.onrender.com

This project is hosted on Render, a modern PaaS chosen for it's simplicity.

# OPTIONAL RESPONSES
Problem 1:
--> img :src="hovered ? drink.images.back : drink.images.front" <--
The above is a line of code I had in my DrinkInfoCard.vue file.

Vue evaluates drink.images.back immediately when rendering the component...
If drink.images is undefined, the fetch hasn’t completed yet, or the JSON hasn’t loaded, it
throws a runtime error.

I learned that I need to instead do this:
:src="hovered ? drink.images?.back : drink.images?.front"

This allows JS to not just immediately error out i.e. the ?. operator tells JavaScript: 
“If drink.images is undefined or null, don’t throw an error; just return undefined.”

So instead of crashing, the img tag’s src becomes undefined.

This is something I got stuck on, and was the source of why nothing was appearing
beneath my welcome message. Vue is a relatively new thing for me and I wanted to make use of it now, as 24G 
mentioned it being their primary framework. I have only used it once before, but it was a very small scale media player I was just fooling around with.

Problem 2:
I ran into an issue when trying to use Google’s Material You close icon for the drink info cards.
To ensure the icon loads correctly after deployment (for example, when hosting on Render),
 you need to dynamically import the SVG like this:

<script setup>
    import CloseIcon from '@/assets/close.svg'
</script>

<button class="close" @click="$emit('close')">
    <img :src="CloseIcon" alt="Close" width="24" height="24" />
</button>

The above approach is necessary since Vite needs to correctly process the asset path during the build,
so the icon’s file path resolves properly in the hosted environment.

Final Thoughts:
Vue.js is really cool and I am glad that I picked this up now it is a good framework and actually is much easier than
using just straight vanilla JavaScript. I didn't realize how nice a framework could be.

Another huge thing I got from this, is I now fully understand what Vite is and how amazing it is
that you can npm run dev and dynamically see changes. I understand that strong vanilla JS skills are the essential
foundation for mastering any framework, and I'm eager to continue building on this by diving deeper into Vue. My goal
is to master one framework well before exploring others!
