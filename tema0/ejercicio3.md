En este ejercicio vamos a poner en marcha un servidor web dummy con código de Python en un entorno de desarrollo.

Para ello tenemos que tener instalado Python y un entorno de desarrollo como, en mi caso, *Visual Studio Code*.
Una vez instalado, crearemos un archivo y pegaremos el siguiente código Python -->

```python
import http.server as httpserver
import socketserver

def main(port=None):
	if port is None:
		port = 8000
	handler = httpserver.SimpleHTTPRequestHandler
	try:
		httpd = socketserver.TCPServer(("", port), handler)
		print("serving at port", port)
		httpd.serve_forever()
	except OSError:
		print("Given PORT:{} is unavailable.Try running with diffrent PORT Number!".format(port))

if __name__ == '__main__':
	main()
```

Una vez pegado el código, lo ejecutaremos y podremos confirmar que nuestro servidor web se lanzó correctamente si vemos lo siguiente --> 
[pantalla 2](/tema0/pantalla2.png).

Creando un index.html y almacenándolo junto al archivo ejectuable de python, podremos visualizar nuestra página web como en este ejemplo -->
[pantalla 3](/tema0/pantalla3.png).
