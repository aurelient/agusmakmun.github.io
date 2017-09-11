{% for projet in site.data.projets-m1 %}

- [{{ projet.title }}]({{ projet.url }}) ({{projet.advisor}})

{% endfor %}
