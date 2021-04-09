## django-quill-editor with image-resize



django-quill-editor  @[LeeHanYeong/django-quill-editor](https://github.com/LeeHanYeong/django-quill-editor)

quill-image-resize-module  @[kensnyder/quill-image-resize-module](https://github.com/kensnyder/quill-image-resize-module)

This repo forked from [LeeHanYeong/django-quill-editor](https://github.com/LeeHanYeong/django-quill-editor), add [quill-image-resize-module](https://github.com/kensnyder/quill-image-resize-module)。

By modify the demo proj(`playground`),achieved django-quill-editor resize image.

`quill-image-resize-module@3.0.0/image-resize.min.js` was introduced in the modification by the way of cdn https://cdn.jsdelivr.net/npm/quill-image-resize-module@3.0.0/image-resize.min.js.

### modified

`django-quill-editor/playground/templates/base.html`  line12 add

```html
<head>
  <meta charset="UTF-8">
  <meta name="viewport"
        content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">

  <!-- django-quill-editor Media -->
  {% include 'django_quill/media.html' %}
  <!-- Quill resize-image.js -->
  <!-- image-resize.min.js must import after Quill.js. like this -->
  <script src="https://cdn.jsdelivr.net/npm/quill-image-resize-module@3.0.0/image-resize.min.js"></script>


  <!-- Custom CSS -->
  <link rel="stylesheet" href="{% static 'bootstrap.min.css' %}">
  <link rel="stylesheet" href="{% static 'style.css' %}">
  <title>django-quill-editor</title>
</head>
```

`django-quill-editor/playground/config/settings.py` line101 add

```python
# Quill config
QUILL_CONFIGS = {
    "default": {
        'theme': 'snow',
        'modules': {
            'syntax': True,
            'toolbar': [
                [
                    {'font': []},
                    {'header': []},
                    {'align': []},
                    'bold', 'italic', 'underline', 'strike', 'blockquote',
                    {'color': []},
                    {'background': []},
                ],
                ['code-block', 'link', 'image', 'video'],
                ['clean'],
            ],
            'imageResize': {  # open imageResize
                'displaySize': True
            }
        }
    }
}
```



------

# django-quill-editor

![PyPI](https://img.shields.io/pypi/v/django-quill-editor)

**django-quill-editor** makes [Quill.js](https://quilljs.com/) easy to use on Django Forms and admin sites

- **No configuration required for static files!**
- The entire code for inserting WYSIWYG editor is less than 30 lines
- It can be used in both admin and Django views

![django-quill-editor](https://raw.githubusercontent.com/LeeHanYeong/django-quill-editor/master/_assets/django-quill-editor-sample.png)



## Documentation

The full document is in [https://django-quill-editor.readthedocs.io/](https://django-quill-editor.readthedocs.io/), including everything about how to use the Form or ModelForm, and where you can add custom settings.

Please refer to the **QuickStart** section below for simple usage.



## QuickStart

### Setup

- Install `django-quill-editor` to your Python environment

  > Requires Python 3.7 or higher and Django 3.1 or higher.

  ```shell
  pip install django-quill-editor
  ```

- Add `django_quill` to `INSTALLED_APPS` in `settings.py`

  ```python
  # settings.py
  INSTALLED_APPS = [
      'django.contrib.admin',
      ...
      'django_quill',
  ]
  ```

### Making Model

Add `QuillField` to the **Model class** you want to use.

> 1. App containing models.py must be added to INSTALLED_APPS
> 2. After adding the app, you need to run makemigrations and migrate to create the DB table.

```python
# models.py
from django.db import models
from django_quill.fields import QuillField

class QuillPost(models.Model):
    content = QuillField()
```

### Using in admin

Just register the Model in **admin.py** of the app.

```python
from django.contrib import admin
from .models import QuillPost

@admin.register(QuillPost)
class QuillPostAdmin(admin.ModelAdmin):
    pass
```

![admin-sample](https://raw.githubusercontent.com/LeeHanYeong/django-quill-editor/master/_assets/admin-sample.png)



## Contributing

As an open source project, we welcome contributions.
The code lives on [GitHub](https://github.com/LeeHanYeong/django-quill-editor)



## Distribution (for owners)

### PyPI Release

```shell
poetry install  # Install PyPI distribution packages
python deploy.py
```



### Sphinx docs

```shell
brew install sphinx-doc  # macOS
```

#### Local

```
cd docs
make html
# ...
# The HTML pages are in _build/html.

cd _build/html
python -m http.server 3001
```

 
