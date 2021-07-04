# Bienvenida a la applicación de SHIELD para Admin-Sistemas

Pasos a seguir:
1. Haz un fork del proyecto
2. Descarga el proyecto del repositorio con git
```
git clone https://github.com/joseluisGA/shield
```

3. Crea un entorno virtual
```
cd shield
python -m venv .venv
```

4. Activa el entorno virtual
En Windows:
```
.venv/Scripts/activate.ps1
```
En Unix o MacOS
```
source .venv/bin/activate
```

5. Instala las librerías del `requirements.txt`
```
pip install -r requeriments.txt
```

6. Ejecuta las migraciones
```
python manage.py migrate
```

7. Carga los datos de superheroes del fichero `superheroes.csv`
```
metahumans/management/commands/load_from_csv.py
```
Si da problemas usando el comando load_from_csv, se puede usar el comando
``` 
manage.py loaddata metahumans/fixtures/initial_data.json
```

8. Crea tu propio usuario superuser para poder entrar en el admin de django
```
python manage.py createsuperuser
```

9. Ejecuta el servidor de django para probar la aplicación
```
python manage.py runserver
```

10. Instale la librería de fabric dentro del entorno virtual
```
pip install fabric
```

11. Compruebe y cambia las credenciales de su máquina remota en el fichero fabfile.py en las líneas 16, 17 y 18
```
@task
def development(ctx):
    ctx.user = 'josega'
    ctx.host = '3.21.162.236'
    ctx.connect_kwargs = {"password": "josega"}
```

12. Despliega la aplicación usando Fabric en tu servidor virtualizado con Vagrant
```
fab development deploy
```

13. Si desea desplegar la aplicación en un entorno de producción vaya al fichero fabfile.py y añada un método como este

*cambie los credenciales por lo de su entorno remoto*
```
@task
def production(ctx):
    ctx.user = 'josega'
    ctx.host = '3.21.162.236'
    ctx.connect_kwargs = {"password": "josega"}
```

Después ejecute el siguiente comando
```
fab producction deploy
```

14. El siguiente paso será empaquetar la aplicación y desplegarla utilizando Docker

15. Para instalar Docker en Windows tiene que descargar e instalar la aplicación de escritorio a través del siguiente enlace
https://desktop.docker.com/win/stable/amd64/Docker%20Desktop%20Installer.exe

16. Ahora construye la imagen de la aplicación a través del fichero Dockerfile usando el siguiente comando
```
docker build -t shield .
```

17. Si quiere ver la imagen que ha generado puede usar
```
docker images
```

18. Para lanzar el contenedor a partir de la imagen que acaba de crear, ejecute el siguiente comando
```
docker run shield
```

19. Para que el contenedor sea visible en su red local, y además el proceso se ejecute en segundo plano
```
docker run -d -p 8000:8000 python-docker
```

20. Para comprobar los contenedores que están ejecutándose en la máquina
```
docker ps
```

21. Si quiere parar el contenedor activo 

*Cambie 'sharp_mendeleev' por el nombre que le muestra en el campo NAMES con el comando docker ps*
```
docker stop sharp_mendeleev
```

22. Para reiniciarlo 

*Cambie 'sharp_mendeleev' por el nombre que le muestra en el campo NAMES con el comando docker ps*
```
docker restart sharp_mendeleev
```

23. para eliminarlo

*Cambie 'sharp_mendeleev' por el nombre que le muestra en el campo NAMES con el comando docker ps*
```
docker rm sharp_mendeleev
```

