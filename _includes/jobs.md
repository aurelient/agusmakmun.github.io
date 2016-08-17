## Open Jobs
{% for job in site.data.jobs %}
{% if job.active == 'y' %}

### {{ job.title }}
posted posted-on : {{ job.date }}  
keywords : {{ job.keywords }}

{{ job.desc }}

{% endif %}
{% endfor %}
