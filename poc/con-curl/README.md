# Prueba con curl
Este escenario consiste en que se dispare un workflow cuando ejecutamos enviamos un mensaje mediante curl a un eventsource. El mismo recoje el mensaje lo almacena para que lo levante argo-sensor. Argo-sensor crea un workfloy en el namespace argo. Revisar dentro de trigger el namespace y el serviceaccount.

### Ejercicio sencillo para realizar troubleshooting

```

# Creamos el servicio que escucha el evento
kubectl apply -f event-source.yaml

# Forwardeamos el puerto localmente, caso contrario tendriamos que crear un ingress
kubectl port-forward webhook-eventsource-6cqzz-67cb8fcf48-x57jg 12000:12000 &

# Creamos el sensor que dispara el trigger
kubectl apply -f sensor.yaml

# Enviamos el siguiente evento a Argo Events 
curl -X POST -H "Content-Type: application/json" -d '{"message":"Roldyx crack!!"}' http://localhost:12000/devops-toolkit

# Finalmente podemos ver los logs
kubectl logs --selector app=payload
Esta ultima instruccion deberia generar un pod dentro del namespace argo

```
