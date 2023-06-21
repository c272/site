---
title: c272@blog:~>
---
<!-- Styles for the page. -->
<style>
.codeblog-overview {
    display: flex;
}

.codeblog-logo {
    margin-top: 0.5em;
    margin-bottom: 2em; 
    margin-right: 2em;
    max-width: 12em;
}

.codeblog-logo img, object {
    -webkit-filter: var(--invert-logo-color);
    filter: var(--invert-logo-color);
    max-width: 12em;
    margin-top: 0;
    margin-bottom: 0;
}

.codeblog-coffee-cup {
    display: block;
    max-width: 8em;
    margin-left: auto;
    margin-right: auto;
    margin-bottom: 0.5em;
}

/* Tucks the logo underneath at small widths. */
@media (max-width: 38rem) {
    .codeblog-overview {
        margin-top: 0;
        flex-wrap: wrap;
        justify-content: center;
	}
}
</style>

<div class="codeblog-overview">
<div>

# Various Musings on Code.

Welcome to my programming-oriented blog, where I post about projects I'm working on and tech I'm interested in, as well as my thoughts on industry goings-on. All (rather half-baked) opinions my own.<br>

</div>
<div class="codeblog-logo">
<object type="image/svg+xml" class="codeblog-coffee-cup" data="/img/coffeecup.svg"></object>
<img src="/img/misc/codeblog-logo-text.png">
</div>
</div>