# Static Files

## Configuring a Project for Static Files

First, you'll need to create a folder for your static files.

```bash
mkdir static_files_folder
```

Next, we'll go into that folder and start creating some files.

```bash
cd static_files_folder
```

## Creating an index.html Page

An index.html page is a common place to put your landing page for your site. You can use 
```touch``` to create the file, **or** you can just use an editor to create it inline.

To simply create the file:
```bash
touch index.html
```

To edit it directly:
```bash
nano index.html
```

Here is the content you should include in your first HTML page.

**index.html**:
```html
<html>
    <body>
        This is an HTML file.
    </body>
</html>
```

## Configuring Yaml for Static Files

We'll want to move to our main directory.

```bash
cd ..
```

Next, we'll want to create an app.yaml file. Again, you can edit it in the Cloud Console editor
or directly in the CLI.

```bash
touch app.yaml
```

```bash
nano app.yaml
```

The contents of your app.yaml should be the following:

**app.yaml**:
```yaml
runtime: python39

handlers:
- url: /static
  static_dir: static_files_folder

- url: /.*
  script: auto

```

Note the new capabilities here; we're adding a new handler with a static_dir property.
This will map anything starting with /static in your URL path directly to this folder.


## Creating Your Python File

The new topic we're going to introduce here is the ability to return a ```Response```
object instead of a plain string. This will allow us to set the ```mimetype``` property
to text/plain so that we can distinguish between the HTML response and the plain text
response.

Create the file and edit it in the Cloud Console editor:

```bash
touch main.py
```

Or edit it directly in the CLI:

```bash
nano main.py
```

Your main.py file will contain mostly the same content, but will return a ```Response```
object.

**main.py**:
```python
from flask import Flask
from flask import Response


app = Flask(__name__)

@app.route('/')
def root():
    return Response('This is NOT HTML.', mimetype='text/plain')

if __name__ == '__main__':
    app.run(host='127.0.0.1', port=8080, debug=True)

```