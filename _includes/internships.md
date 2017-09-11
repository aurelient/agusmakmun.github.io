## Internships
Usually posted around November, contact me if you have ideas.

{% for internship in site.data.internships %}
{% if internship.active == 'y' %}

### {{ internship.title }}
<sup>
{{ internship.date }} – {{ internship.keywords }}
</sup>

{{ internship.desc }}

{% endif %}
{% endfor %}
