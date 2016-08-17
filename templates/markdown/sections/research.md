{% extends "section.md" %}

{% block body %}
<table class="table table-hover">
{% for r in items %}
<tr>
  <td class='col-md-3'>{{ r.dates }}</td>
  <td>
    <strong>{{ r.place }}</strong>, {{ r.location }} <br/>
    {% if r.title %} {{ r.title }}, {% endif %}
    {% if r.advisor %}{{ r.advisor }}{% endif %}
    {% if r.title or r.advisor %}.{% endif %}
  </td>
</tr>
{% endfor %}
</table>

{% endblock body %}
