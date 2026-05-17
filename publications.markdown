---
layout: main
title: Publications
permalink: /publications/
---

# Publications

<div class="publication-list">
  {% for publication in site.data.publications %}
    {% include publication.html publication=publication %}
  {% endfor %}
</div>
