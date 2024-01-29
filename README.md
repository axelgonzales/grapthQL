# Explicación de la solución
Se creo nos microservicios uno para generar la transación y hacer el registro y actualización en la base de datos de Postgress
y el otro para hacer la validación de antifraude donde las transacciones no tenian que ser mayores a 1000.
Para la comunicación entre ellos se utilizo kafka.
Donde los pasos de ejecución fueron los siguientes 

<ol>
  <li>A traves de GraphQL se crea una transaccción</li>
  <li>Desde el primer microservicio (transacción) se guarda la transacción en la base de datos</li>
  <li>Desde el primer microservicio  (transacción) se crea un evento con el topic "antifraud-request" para validar el antifraude de la transacción se</li>
  <li>Desde el segundo microservicio  (antifraude) se subscribe al topic "antifraud-request"</li>
  <li>Desde el segundo microservicio  (antifraude) se evalua la transacción si es mayor a 1000</li>
  <li>Desde el segundo microservicio  (antifraude) se crea el evento de respuesta en el topic "antifraud-pull"</li>
  <li>Desde el primer microservicio  (transacción) se subscribe al topic "antifraud-pull"</li>
  <li>Desde el primer microservicio  (transacción) se actualizo el registro de esa transacción con el status de respuesta</li>
</ol>

# Herramientas utilizadas
Las tecnologias que se usaron fueronh
<ol>
   <li>NodeJs</li>
   <li>Nestjs</li>
   <li>TypeOrm</li>
   <li>GraphQL</li>
   <li>Kafka</li>
   <li>PostgreSQL</li>
</ol>
# Instrucciones de Configuración y Ejecución

## Configuración del Proyecto

### Paso 1: Iniciar Servicios Docker
En la raíz del proyecto, ejecuta el siguiente comando para iniciar los servicios Docker:

docker-compose up

### Paso 2: Configuración del Servicio de Antifraude
<ol>
  <li>Dirígete a la carpeta antifraude.</li>
  <li>Instala las dependencias ejecutando:
       npm install
</li>
  <li>Inicia el servicio con el siguiente comando:
       npm run start
  </li>  
</ol>


### Paso 3: Configuración del Servicio de Transacción
<ol>
  <li>Dirígete a la carpeta transaction</li>
  <li>Instala las dependencias ejecutando:
       npm install
</li>
  <li>Inicia el servicio con el siguiente comando:
       npm run start
  </li>  
</ol>

### Paso 4: Importar la colección postman para pruebas
Desde postman seleccione la opción de importar y arrastre el siguiente archivo colocado en la raiz del proyecto
Prueba Yape GPL.postman_collection.json

### Notas Adicionales
Si encuentras algún problema durante la configuración o ejecución, consulta la documentación del proyecto o comunícate con el equipo de desarrollo para obtener ayuda.
