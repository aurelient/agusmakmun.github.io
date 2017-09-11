{% extends "section.md" %}

{% block body %}
<table class="table table-hover">
{% for project in items %}
<tr>
  {% if project.url %}
  <td class='col-md-3'><a href="{{ project.url }}">{{ project.name }}</a></td>
  {% else %}
  <td class='col-md-3'>{{ project.name }}</td>
  {% endif %}
  <td>
    {{ project.status }}, {{ project.duration }} <br/>
    {% for detail in project.details %}
    <p>{{ detail }}</p>
    {% endfor %}
  </td>
</tr>
{% endfor %}
</table>

{% endblock body %}
