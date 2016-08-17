<h3> <a class="smaller" name="{{ name }}"><i class="fa fa-chevron-right smaller"></i></a> {{ name }} </h3>
{% if legend %}
{{ legend }}
{% endif %}

{% block body %}
{{ data }}
{% endblock body %}
