---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: main
---
<section class="home-section intro-section" markdown="1">
I'm a third year PhD student in Machine Learning at the **University of Oxford**, supervised by [Prof Michael Bronstein](https://www.cs.ox.ac.uk/people/michael.bronstein/){:target="_blank"}, [Dr İsmail Ceylan](https://www.cs.ox.ac.uk/people/ismaililkan.ceylan/){:target="_blank"}, and [Dr Joey Bose](https://joeybose.github.io/){:target="_blank"}. I am currently interning at **Apple MLR** under the supervision of [Prof Marco Cuturi](https://marcocuturi.net/){:target="_blank"}.

My work primarily focuses on **generative modelling**. In particular, I am most interested in:

- Diffusion & flow matching;
- Accelerated methods (*e.g.*, flow maps), and controlled generation;
- Continuous processes for language generation (Categorical Flow Maps).
</section>

<section class="home-section bio-section" markdown="1">
<div class="section-kicker">Education & Experience</div>

I hold a BSc in Computer Science from EPFL with an exchange year at Imperial College London, and an MSc in Advanced Computer Science from the University of Oxford. I was also awarded the **Tony Hoare Prize** for the **best MSc thesis of the year**, *Information Theoretic Perspectives on Graph Neural Networks*.

Currently, I am interning at Apple MLR. I have previously worked at Microsoft Research, and Genesis Molecular AI.

My PhD funding is generously provided by both [Project CETI](https://www.projectceti.org/){:target="_blank"} and Intel.
</section>

# Selected Publications

<div class="publication-list publication-list-featured">
  {% assign selected_publications = site.data.publications | where: "selected", true %}
  {% for publication in selected_publications %}
    {% include publication.html publication=publication featured=true %}
  {% endfor %}
</div>

<p class="section-link"><a href="{{ '/publications/' | relative_url }}">View all publications</a></p>
