# Argo Events

### Funcionamiento

git push -> [ Repo de Aplicación] -> Gitlab webhook -> Argo Events (EventSource) -> Argo Events (Sensors)

### Ejercicio con Webhook de Github
**NOTA IMPORTANTE** El webhook se hace sobre la aplicacion que queremos construir, NO SOBRE LOS MANIFIESTOS

* Creamos un webhook para el proyecto argo-events
```shell
https://github.com/roldyxoriginal/helloworld/settings/hooks/
seleccionamos que sea JSON
``` 

* Luego dentro de nuestro repo helloworld (codigo fuente de nuestra aplicacion)

```shell
echo "* Prueba 23">>README.md;git add . ; git commit -m "prueba23";git push

```


