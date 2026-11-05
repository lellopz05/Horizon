---
layout: default
title: Home
---

# Horizon

AI-curated daily digest of tech and research news, built from
[this repository](https://github.com/lellopz05/Horizon).

## Daily Digest

<ul>
  {% for post in site.posts limit:20 %}
    <li><a href="{{ post.url | relative_url }}">{{ post.date | date: "%Y-%m-%d" }}</a></li>
  {% else %}
    <li><em>No briefings yet</em></li>
  {% endfor %}
</ul>

[RSS feed]({{ '/feed.xml' | relative_url }})

## Documentation

- [Configuration Guide](configuration) — AI providers, sources, filtering, environment variables
- [Source Scrapers](scrapers) — what Horizon collects and how
- [Scoring System](scoring) — the 0-10 rubric per profile
