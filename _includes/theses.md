
## Master theses
{% for thesis in site.data.theses %}
{% if thesis.active == 'y' %}

### {{ thesis.title }}
posted on : {{ thesis.posted-on }}  
keywords: {{ thesis.keywords }}

{{ thesis.desc }}

{% endif %}
{% endfor %}


<!-- ## Completed theses
... -->
