## Internships
{% for internship in site.data.internships %}
{% if internship.active == 'y' %}

### {{ internship.title }}
posted posted-on : {{ internship.date }}  
keywords : {{ internship.keywords }}

{{ internship.desc }}

{% endif %}
{% endfor %}
