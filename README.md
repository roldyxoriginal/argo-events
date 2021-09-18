# Argo Events

### Funcionamiento

**Event Source - Servicio que recibe eventos**
Se crea lo que se llama un event source(eventsource) que basicamente es un servicio que expone un puerto que atiende un evento que puede ser un POST http con Curl o un evento generado desde gitlab o github. Este eventsource por defecto no hace nada, solo recibe el mensaje y devuelve success si lo recibio bien.
Aca estan todos los clientes que pueden enviarles eventos.

https://github.com/argoproj/argo-events/blob/master/api/event-source.md#eventsourcespec
Ejemplos:
https://github.com/argoproj/argo-events/tree/master/examples/event-sources


**Event Sensor - Servicio que realiza una acción(trigger)**
Se utiliza para disparar una accion, la misma se encuentra diseñada dentre de un manifiesto de "Kind: Sensor". Un trigger es un spec del Sensor.

### Instalacion 

```
kubectl create namespace argo-events
kubectl apply -n argo-events -f https://raw.githubusercontent.com/argoproj/argo-events/stable/manifests/namespace-install.yaml
kubectl apply -n argo-events -f https://raw.githubusercontent.com/argoproj/argo-events/stable/examples/eventbus/native.yaml
```

### Ejercicio

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

```

**NOTA: No funciona la instalacion con HELM 3(por ahora)**

### Ejercicio con Webhook de Github
Creamos un webhook para el proyecto argo-events
https://github.com/roldyxoriginal/argo-events/settings/hooks/
