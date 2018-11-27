{% assign past_year = 0 %}

## Ph.D. Students
{% for student in site.data.students %}
{% if student.active == 'y' %}
### {{student.name}}
{{student.title}}, {{student.desc}}
{% endif %}

{% endfor %}


## Former Ph.D. Students
{% for student in site.data.students %}
{% if student.active == 'n' %}
### {{student.name}}
{{student.title}}, {{student.desc}}

{% endif %}
{% endfor %}
