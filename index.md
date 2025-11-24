---
layout: page
title: "Home"
class: home
---
<!-- 
# Hi, I'm Ziao Liu -->

<div class="columns" markdown="1">

<div class="intro" markdown="1">
I'm Ziao Liu (刘子奥), a third-year PhD student at Zhejiang University (ZJU). I'm a member of the <a href='https://zjuidg.org'>ZJUIDG</a> Lab, co-supervised by Prof. {% include person person="Xiao Xie" %}, Prof. {% include person person="Hui Zhang" %}, and Prof. {% include person person="Yingcai Wu" %}. I received my bachelor's degree of Data Science and Big Data Technology at Chongqing Univeristy (CQU), where I was supervised by Prof. {% include person person="Haibo Hu" %} and was part of the CQU-VIVA Lab.

My research focuses on data visualization and human-computer interaction (HCI) within the domain of sports. Currently, I am exploring the integration of large language models (LLMs) into sports analytics, particularly applying them in tactical and strategy analysis.

<time class="status-date" datetime="{{ site.time | date: '%Y-%m-%d' }}">{{ site.time | date: "%b %d, %Y" }}</time> I am currently seeking visiting positions.

</div>

<div class="me" markdown="1">
<picture>
  <img
    src='/images/ziao.jpg'
    alt='Ziao Liu'>
</picture>

{:.no-list}

- <a href="mailto:{{ site.email }}">{{ site.email }}</a>
</div>

</div>

## News

<div class="news-scrollable">
  <ul class="news-list">
    {% assign sorted_news = site.data.news | sort: 'date' | reverse %}
    {% for news_item in sorted_news %}
      {% assign news = news_item %}
      {% include news.html %}
    {% endfor %}
  </ul>
</div>

##  <a href="{{ "/publications/" | relative_url }}">Publications</a>

<div class="featured-publications">
  {% assign sorted_publications = site.publications | sort: 'month' | reverse | sort: 'year' | reverse %}
  {% assign featured_publications = sorted_publications | where: 'highlight', true %}
  {% if featured_publications == empty %}
    {% assign featured_publications = sorted_publications | slice: 0, 3 %}
  {% endif %}
  {% for pub in featured_publications %}
    {% assign anchor = pub.id | default: pub.title | slugify %}
    {% assign primary_link = pub.pdf %}
    {% unless primary_link %}
      {% assign primary_link = pub.link %}
    {% endunless %}
    {% unless primary_link %}
      {% assign primary_link = pub.html %}
    {% endunless %}
    {% unless primary_link %}
      {% assign primary_link = pub.video %}
    {% endunless %}
    {% unless primary_link %}
      {% assign primary_link = pub.slides %}
    {% endunless %}
    {% unless primary_link %}
      {% assign primary_link = pub.doi %}
    {% endunless %}
    {% unless primary_link %}
      {% assign primary_link = "/publications/#" | append: anchor %}
    {% endunless %}
    <article class="publication-card">
      <a class="thumb" href="{{ primary_link }}" aria-label="Open {{ pub.title }}">
        <img src="{{ pub.thumbnail | default: '/images/ziao.jpg' | relative_url }}" alt="{{ pub.title }} thumbnail">
      </a>
      <div class="info">
        <h3><a href="{{ primary_link }}">{{ pub.title }}</a></h3>
        <p class="authors">{% for author in pub.authors %}{% include person person=author %}{% unless forloop.last %}, {% endunless %}{% endfor %}</p>
        <p class="meta">
          {% if pub.venue %}<span class="venue-tag">{{ pub.venue }}</span>{% endif %}
          {% if pub.year %}{{ pub.year }}{% endif %}
          {% if pub.type %} · {{ pub.type | join: ", " }}{% endif %}
        </p>
        {% if pub.summary %}
          <p class="summary">{{ pub.summary }}</p>
        {% endif %}
        {% if pub.awards %}
          <div class="awards">
            {% for award in pub.awards %}
              <span><i class="fas fa-{% if award == "Best Paper" %}trophy{% else %}award{% endif %}" aria-hidden="true"></i> {{ award }}</span>
            {% endfor %}
          </div>
        {% endif %}
        {% if pub.link or pub.pdf or pub.video or pub.blog or pub.slides or pub.doi or pub.arxiv %}
          <div class="actions">
            {% if pub.pdf %}
              <a href="{{ pub.pdf }}">
                <i class="far fa-file-pdf" aria-hidden="true"></i> PDF
              </a>
            {% elsif pub.arxiv %}
              <a href="https://arxiv.org/pdf/{{ pub.arxiv | cgi_escape }}.pdf">
                <i class="far fa-file-pdf" aria-hidden="true"></i> PDF
              </a>
            {% endif %}
            {% if pub.link %}
              <a href="{{ pub.link }}">
                <i class="fas fa-link" aria-hidden="true"></i> Project
              </a>
            {% endif %}
            {% if pub.html %}
              <a href="{{ pub.html }}">
                <i class="fab fa-html5" aria-hidden="true"></i> HTML
              </a>
            {% elsif pub.arxiv %}
              {% if pub.year >= 2024 %}
              <a href="https://arxiv.org/html/{{ pub.arxiv | cgi_escape }}v1">
              {% else %}
              <a href="https://ar5iv.org/html/{{ pub.arxiv | cgi_escape }}">
              {% endif %}
                <i class="fab fa-html5" aria-hidden="true"></i> HTML
              </a>
            {% endif %}
            {% if pub.blog %}
              <a href="{{ pub.blog }}">
                <i class="fas fa-newspaper" aria-hidden="true"></i> Article
              </a>
            {% endif %}
            {% if pub.video %}
              <a href="{{ pub.video }}">
                <i class="fas fa-film" aria-hidden="true"></i> Video
              </a>
            {% endif %}
            {% if pub.recording %}
              <a href="{{ pub.recording }}">
                <i class="fas fa-video" aria-hidden="true"></i> Recording
              </a>
            {% endif %}
            {% if pub.slides %}
              <a href="{{ pub.slides }}">
                <i class="fas fa-window-maximize" aria-hidden="true"></i> Slides
              </a>
            {% endif %}
            {% if pub.doi %}
              <a href="https://www.doi2bib.org/bib/{{ pub.doi }}">
                <i class="fas fa-book" aria-hidden="true"></i> Bibtex
              </a>
            {% elsif pub.arxiv %}
              <a href="https://arxiv2bibtex.org/?q={{ pub.arxiv | cgi_escape }}">
                <i class="fas fa-book" aria-hidden="true"></i> Bibtex
              </a>
            {% endif %}
            {% if pub.short_doi %}
              <a href="http://doi.org/{{ pub.short_doi }}">
                <i class="fas fa-anchor" aria-hidden="true"></i> DOI: {{ pub.short_doi }}
              </a>
            {% endif %}
            {% if pub.arxiv %}
              <a href="https://arxiv.org/abs/{{ pub.arxiv }}">
                <i class="fas fa-archive" aria-hidden="true"></i> arXiv: {{ pub.arxiv }}
              </a>
            {% endif %}
            {% if pub.osf %}
              <a href="https://osf.io/{{ pub.osf }}">
                <i class="fas fa-archive" aria-hidden="true"></i> OSF: {{ pub.osf }}
              </a>
            {% endif %}
          </div>
        {% endif %}
      </div>
    </article>
  {% endfor %}
</div>

<a href="{{ "/publications/" | relative_url }}" class="button">
<i class="fas fa-chevron-circle-right"></i>
Show All Publications
</a>
