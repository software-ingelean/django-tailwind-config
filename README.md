# django-tailwind-config


## Configuración inicial

Crea el proyecto de Django

Instala `django-compressor`:
```bash
pip install django-compressor
```

Agregalo a installed apps de `settings.py`:
```python
# config/settings.py

INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'compressor',  # new
]
```

Configura `compressor` en el `settings.py`:

```python
# config/settings.py

# DJANGO COMPRESSOR
COMPRESS_ROOT = BASE_DIR / 'static'
COMPRESS_ENABLED = True
STATICFILES_FINDERS = [
    'django.contrib.staticfiles.finders.FileSystemFinder',
    'django.contrib.staticfiles.finders.AppDirectoriesFinder',
    'compressor.finders.CompressorFinder',
]
```

Crea un archivo `input.css` dentro de la carpeta `static/src/`:
```
static
└── src
    └── input.css
```

Crea una carpeta `frontend/` en la raiz del proyecto para instalar todo lo relacionado con el frontend:
```bash
cd frontend/
```
## Instalación de **TailwindCSS**

Instalando `TailwindCSS`:
```bash
npm install -D tailwindcss
npx tailwindcss init
```

Al instalar e inicializar `TailwindCSS` en la carpeta `frontend/` tuvo que haber quedado algo como esto:

```
frontend
└── node_modules/
└── package.json
└── package-lock.json
└── tailwind.config.js

```

Agrega las rutas a todos sus archivos de plantilla en el archivo `tailwind.config.js`:

```javascript
module.exports = {
  content: [
    "../templates/**/*.html",
    "../static/js/**/*.js",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}
```

Agregue las directivas `@tailwind` para cada una de las capas de Tailwind a su archivo CSS principal `static/src/input.css`:
```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

Ejecute `tailwindCSS` desde la carpeta `frontend/`:

```bash
npx tailwindcss -i ../static/src/input.css -o ../static/src/output.css --watch
```


Importe en su template el archivo `output.css` que genera tailwind:

```html
{% compress css %}
    <link rel="stylesheet" href="{% static 'src/output.css' %}" />
{% endcompress %}
```

## Integración con **Flowbite**

Instala `Flowbite`:

```bash
npm install flowbite
```

Agrega `Flowbite` como complemento dentro del archivo `tailwind.config.js`:

```javascript
module.exports = {
  content: [
    "../templates/**/*.html",
    "../static/js/**/*.js",
    "./node_modules/flowbite/**/*.js", // Agrega esto
  ],
  darkMode: "class",
  theme: {
    extend: {},
  },
  plugins: [require("flowbite/plugin")], // Agrega esto
};
```

Incluya el archivo JavaScript de Flowbite dentro del archivo `_base.html` justo antes del final de la etiqueta usando CDN o incluyéndolo directamente desde la carpeta node_modules/:

```html
<script src="https://cdn.jsdelivr.net/npm/flowbite@2.5.2/dist/flowbite.min.js"></script>
```
