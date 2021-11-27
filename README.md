# Argo Events

### Funcionamiento

git push -> [ Repo de Aplicación] -> Gitlab webhook -> Argo Events (EventSource) -> Argo Events (Sensors)

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
kubectl apply -k install
```


**NOTA: No funciona la instalacion con HELM 3(por ahora)**

# Url adicionales
https://github.com/vfarcic/argo-combined-demo
https://github.com/vfarcic/argo-combined-app
