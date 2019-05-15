---
layout: post
title: Quick Tips and Tricks for Hugo Development
date: '2019-05-15'
description: A look at some simple but overlooked as well as some advanced techniques for the Hugo static site generator.
categories:
  - static sites
  - web development
comments: true
---

[Hugo](https://gohugo.io/) is a really powerful static site engine built in Go. I've used it in various projects including using it to build the site for the [events I run](https://cfe.dev/) (which includes my free online monthly meetups). It was pretty basic, as I didn't know at the time where this would all lead. Finally, two years later I am taking the time to properly rebuild the site (though it isn't live yet) and, in the process, am learning a lot of new things about Hugo.

While I commend Hugo on documentation that includes a host of usable example templates and code, this post shares some of the things I've learned so far while building this site that expand a bit on what is in the documentation. I should note that there may be better ways to do some of the things I am doing, so, if any of you are Hugo experts, I'd love to hear ideas for improvement.

## Basic Pagination

Hugo provides configuration and an object (`.Paginator`) to assist in [pagination](https://gohugo.io/templates/pagination/). The default number of items on a paginated list page is 10, but in my case I only wanted 5. In order to do that, I changed the setting in my `config.yaml`.

```yaml
paginate: 5
```

Beneath the list of items on the page there was a list of pages by number, as well as a back and forward button. What I wanted to do was show the navigation if there was more than one page, the back button only if there were previous pages and the forward button only if there were subsequent pages. Finally, the current page would have different styling and not be linked.

```html
{% raw %}{{ if gt .Paginator.TotalPages 1}}
  <!-- Pagination -->
  <nav class="pagination">
    {{ $paginator := .Paginator }}
    {{ if .Paginator.HasPrev }}
    <a href="{{ .Paginator.Prev.URL }}" class="pagination__page pagination__icon pagination__page--next"><i class="ui-arrow-left"></i></a>
    {{ end }}
    {{ range .Paginator.Pagers }}
      {{ if eq .PageNumber $paginator.PageNumber }}
    <span class="pagination__page pagination__page--current">{{ .PageNumber }}</span>
      {{ else }}
    <a href="{{ .URL }}" class="pagination__page">{{ .PageNumber }}</a>
      {{ end }}
    {{ end }}
    {{ if .Paginator.HasNext }}
    <a href="{{ .Paginator.Next.URL }}" class="pagination__page pagination__icon pagination__page--next"><i class="ui-arrow-right"></i></a>
    {{ end }}
  </nav>
  {{ end }}
</div>{% endraw %}
```

The first line of the above code checks if we have more than one total pages. `.Paginator.HasPrev` is used to determine if a previous paginated page exists and `.Paginator.HasNext` if a next page exists. Likewise `.Paginator.Prev` contains the preceding paginated page object and `.Paginator.Next` the next page object. `.Paginator.Pagers` contains all of the paginated pages to iterate through.

One quirk you may notice is that I set a variable with the paginator. Why? Well, it allows me to compare `.PageNumber` of the paginated page object when iterating to the page number of the current page object to me to properly highlight the current page on the navigation. 

## Get Posts by Date

This is a bit of a quirk related to the type of site I am creating. In my site, there are future events (that are future data, thus I need to use the `--buildFuture` flag when building) and past events that are recorded. This kind of query though could also be useful if you want to get posts within a date range perhaps. The end result was actually quite simple, but I will admit to trying a ton of different attempts to get this to work and failing.

In the first case, the only future dated posts on my site are events, so I just query for pages with a date greater than `now`. I set this in a variable so that I can check if it is empty and display a message if it is. Otherwise, I just iterate through and display upcoming items.

```html
{% raw %}{{ $upcoming := where .Site.RegularPages ".Date" "ge" now }}
{{ if ne (len $upcoming) 0 }}
	{{ range $upcoming }}
		<!-- display upcoming events -->
	{{ end }}
{{ else }}
	<p>Shoot! There are no upcoming events</p>
{{ end }}{% endraw %}
```
The query for past events is a little trickier since I need to select only pages in the events section. In this case, I just need to nest my [where functions](https://gohugo.io/functions/where/).

```html
{% raw %}{ $recorded := where (where .Site.RegularPages ".Date" "le" now) "Section" "events" }}
{{ if ne (len $recorded) 0 }}
	{{ range $recorded }}
		<!-- display recorded events -->
	{{ end }}
{{ else }}
	<p>Shoot! There are no recorded events</p>
{{ end }}{% endraw %}
```

## Shortcodes

This one is pretty simple and well covered in the [documentation](https://gohugo.io/content-management/shortcodes/), but I mention it because it's a feature that can be easily overlooked. Shortcodes are useful for when I want to be able to be able to display something within Markdown generated content that is more complicated than what Markdown can handle. For example, Hugo has some [built-in shortcodes](https://gohugo.io/content-management/shortcodes/#use-hugo-s-built-in-shortcodes) for things like adding Gists, highlighting code or much more.

In my case, I want to be create a custom shortcode to display a list of the recorded events that I created above. The first thing I do is place the template for this within `/layouts/shortcodes/`. In this case, imagine I named the file `recorded-events.html`. Next I can just call it from within the Markdown of the page.

```html
{% raw %}{{% recorded-events %}}{% endraw %}
```

Shortcodes actually support passing parameters, which makes them much more powerful than what I show here, but I just want to ensure you are aware of the feature.

## Menu Navigation

Maintaining menu navigation can get tricky, which is why Hugo provides a [menu object](https://gohugo.io/templates/menu-templates/) to help you manage it. You can have multiple navigation menus. In my case, I have two defined in `config.yaml`: "main" and "top". (Yes, I am super creative at naming them!)

```yaml
menu: ["main", "top"]
```

If I wanted to, I could define the menus further within the configuration, but, in my case, I wanted to navigation to create a drop down of recorded events. This list would be limited to the most recent ten events, after which it would just link you to the page with the full listing of past events.

In this case, I relied on defining the navigation within the front matter of each page. For example, here's the relevant front matter from my past April meetup:

```yaml
menu:
  main:
    parent: "events"
    name: "April 2019"
```

This says that it is in the main menu, under "events" (which is the identifier for the "Recorded Events" menu item). Now I just need to iterate through the most recent 10, so I use a sort to sort on the child page object's date descending.

```html
{% raw %}{{ $currentPage := . }}
{{ range .Site.Menus.main }}
    {{ $parentNavURL := .URL }}
    <li{{ if .HasChildren }} class="nav__dropdown"{{ end }}>
    <a href="{{ .URL }}">{{ .Name }}</a>
    {{ if .HasChildren }}
    <ul class="nav__dropdown-menu">
        {{ $children := sort .Children ".Page.Date" "desc" }}
        {{ range first 10 $children }}
        <li><a href="{{ .URL }}">{{ .Name }}</a></li>
        {{ end }}
        {{ if gt .Children 10 }}
        <li><a href="{{ $parentNavURL }}">More...</a></li>
        {{ end }}
    </ul>
    {{ end }}
    </li>
{{ end }}{% endraw %}
```

In this case, I set a variable `parentNavURL` to the parent's URL (i.e. the "Recorded Events" menu item) so that I can create a menu item of "More..." to link to the list of all recorded events. I then iterate through only the first 10 and display the "More..." link only if there are more than 10 children.

One side note, I couldn't a way to dynamically add events to the upcoming or recorded menu despite several attempts. Thus, I am now manually swapping these in the navigation.

## Next/Previous Page Navigation

When you are viewing a post (or, in my case, event), it might be useful to be able to navigate directly to the next or previous post. Hugo makes this pretty easy via some properties on the page object. Here's the relevant code from my template.

```html
{% raw %}<!-- Prev / Next Post -->
<nav class="entry-navigation">
	<div class="clearfix">
	{{ if ne .PrevInSection  nil }}
	<div class="entry-navigation--left">
		<i class="ui-arrow-left"></i>
		<span class="entry-navigation__label">Previous Event</span>
		<div class="entry-navigation__link">
		{{ with .PrevInSection }}
		<a href="{{.Permalink}}" rel="next">{{ .Title }}</a>
		{{ end }}
		</div>
	</div>
	{{ end }}
	{{ if ne .NextInSection  nil }}
	<div class="entry-navigation--right">
		<span class="entry-navigation__label">Next Event</span>
		<i class="ui-arrow-right"></i>
		<div class="entry-navigation__link">
		{{ with .NextInSection }}
		<a href="{{ .Permalink }}" rel="prev">{{ .Title }}</a>
		{{ end }}
		</div>
	</div>
	{{ end }}
	</div>
</nav>{% endraw %}
```

`. PrevInSection` gives you the page object for the previous page within the same site section. If it doesn't exist, it will be null (`nil` in the case of Go). The `with .PrevInSection` simply allows me to use the shorthand dot-notation for the object properties (i.e. use `.Permalink` rather than `.PrevInSection.Permalink`).

## Related Posts

Hugo has built-in support for [related content](https://gohugo.io/content-management/related/). It includes default configuration for how it determines if an item is related, but, in my case, I had to customize it a bit within `config.yaml`. The key difference was that I relied primarily on the categories property of each page to determine if it was related and I wanted to include newer pages as I would like to recommend the current event, for instance, if you are viewing a related older event.

```yaml
related:
  threshold: 80
  includeNewer: true
  toLower: false
  indices:
  - name: categories
    weight: 100
  - name: date
    weight: 10
```

Displaying the related pages is pretty simple within my template. In my case, I want to display the top five related pages to the current page.

```html
{% raw %}{{ $related := .Site.RegularPages.Related . | first 5 }}
{{ with $related }}
{{ range . }}
	<!-- display related items -->
{{ end }}{% endraw %}
```
In the case of the above code, the `.` after `.Site.RegularPages.Related` is an argument passed to that function (i.e. `Related`) that to the current page object. The `| first 5` is a filter that limits the results. Again, `with $related` just lets me use the shorthand dot-notation within my iteration.

## Display Relative Age

For my final item (at least, so far), when listing past events in certain locations, I wanted to display the relative age of an event rather than just the date.

```html
{% raw %}{{ $ageDays := div (sub now.Unix .Date.Unix) 86400 }}
{{ $ageMonths := div (sub now.Unix .Date.Unix) 2592000 }}
{{ $ageYears := math.Floor (div $ageMonths 12) }}
<li class="entry__meta-date">
{{ if lt $ageDays 0 }}
	{{ $ageDays := mul $ageDays -1 }}
	In {{ $ageDays }} {{ cond (eq $ageDays 1) "day" "days"}}
{{ else if ge $ageYears 1 }}
	{{ $ageYears }} {{ cond (eq $ageYears 1) "year" "years" }} ago
{{ else if eq $ageDays 0 }}
	Today
{{ else if lt $ageDays 31 }}
	{{ $ageDays }} {{ cond (eq $ageDays 1) "day" "days"}} ago
{{ else }}
	{{ $ageMonths }} {{ cond (eq $ageMonths 1) "month" "months" }} ago
{{ end }}
</li>{% endraw %}
```

The gist of this is easy. First I create variables that determine the age in days, months and years of the page. Then, utilizing various function provided by Hugo, I display these. For example, since I have events that are future dated, some of them can come back with a negative age. Thus, if the age in days is less than 0, I multiply (using `mul`) by negative one. I also use `cond` to display either the singular or plural based on the condition.

## More to come...

As I said, I am not quite done with this site redesign. If I gain any more insights, I'll be sure to share. Hopefully this is useful for some of you researching how to do things in Hugo. If you have any tips or any suggestions on how I could do the above better, let me know.