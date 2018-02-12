---
title: "Publicar y consumir código Python | Documentos de Microsoft"
ms.custom: 
ms.date: 11/09/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: python
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 8720440872fb0b41a76d4ac644fd3b60d52a095e
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2018
---
# <a name="publish-and-consume-python-web-services"></a>Publicar y consumir servicios web de Python
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Puede implementar una solución de Python y en funcionamiento en un servicio web mediante la característica de puesta en marcha en el servidor de aprendizaje de máquina de Microsoft. En este tema se describe los pasos para publicar correctamente y, a continuación, ejecutar la solución.

La audiencia de destino para este artículo es científicos de datos que desean obtener información sobre cómo publicar código Python o modelos como servicios web hospedados en el servidor de aprendizaje de máquina de Microsoft. El artículo también explica cómo las aplicaciones pueden consumir el el código o los modelos. Este artículo se supone que son expertos en Python.

> [!IMPORTANT]
>
> Este ejemplo se desarrolló para la versión de Python que se incluye con el servidor de aprendizaje de máquina (independiente) y utiliza las características de la versión del servidor de aprendizaje de máquina **9.1.0**.
 > 
 > Haga clic en el vínculo siguiente para ver el mismo ejemplo, volver a publicar mediante las bibliotecas más recientes en el servidor de aprendizaje de máquina. Vea [implementar y administrar servicios web de Python](https://docs.microsoft.com/machine-learning-server/operationalize/python/how-to-deploy-manage-web-services).

**Se aplica a: Microsoft R Server (independiente)**

## <a name="overview-of-workflow"></a>Información general del flujo de trabajo

El flujo de trabajo de publicación para consumir un servicio web de Python, se puede resumir de la siguiente manera:

1. Cumplir los [prerequisite](#prereq) consiste en generar la biblioteca de cliente de Python del documento de Swagger de la API de núcleo.
2. Agregar lógica de autenticación y el encabezado en el script de Python.
3. Crear una sesión de Python, preparar el entorno y crear una instantánea para mantener el entorno.
4. Publicar el servicio web y lo inserte esta instantánea.
5. Probar el servicio web, puede usarlo en la sesión.
6. Administrar estos servicios.

![Flujo de trabajo de swagger](./media/data-scientist-python-workflow.png)

En este artículo se describe cada paso del flujo de trabajo e incluye código de Python de ejemplo con el conjunto de datos de iris.

## <a name="sample-code"></a>Código de ejemplo

Este código de ejemplo se da por supuesto que se han cumplido los [requisitos previos](#prereq) para generar una biblioteca de cliente de Python desde ese Swagger archivo y que han usado Autorest.

Después del bloque de código, encontrará un tutorial paso a paso con descripciones más detalladas del proceso completo.

> [!IMPORTANT]
> Este ejemplo utiliza la variable local `admin` cuenta para la autenticación. Sin embargo, debería sustituir las credenciales y [método de autenticación](#python-auth) configurado por el administrador.

```python
##################################################
##       IMPORT GENERATED CLIENT LIBRARY        ##
##################################################

# Import the generated client library. 

import deployrclient

# This example is intended for use with Microsoft R Server 9.0.1. 
# If you are using a newer version of Machine Learning Server, 
# use the mrs_server library instead.

##################################################
##              AUTHENTICATION                  ##
##################################################

#Using client library generated from Autorest
#Create client instance and point it at an R Server. 
#In this case, R Server is local.
client = deployrclient.DeployRClient("http://localhost:12800")
# To use ML Server, replace with mrs_server.MRSServer()

#Define the login request and provide credentials 
#Update values with the connection parameters from your admin
login_request = deployrclient.models.LoginRequest("<<your-username>>","<<your-password>>")

#Make a call to the /login API. 
#Store the returned an access token in a variable.
token_response = client.login(login_request)

#Add the returned access token to the headers variable.
headers = {"Authorization": "Bearer {0}".format(token_response.access_token)}

#Verify that the server is running.
#Remember to include `headers` in all requests!
status_response = client.status(headers) 
print(status_response.status_code)


##################################################
##        CREATE SESSION, MODEL, SNAPSHOT       ##
##################################################

#Since already logged in, create a Python session.
#Define session using name (`Session 1`) and `runtime_type="Python"`.
#Remember to specify the Python runtime type.
create_session_request = deployrclient.models.CreateSessionRequest("Session 1", runtime_type="Python")

#Make the call to start the session. 
#Remember to include headers in all method calls to the server.
#Returns a session ID.
response = client.create_session(create_session_request, headers) 
   
#Store the session ID in a variable called `session_id` 
#to be able to identify it later at execution time.
session_id = response.session_id

#Create model - Import SVM and datasets from the SciKit-Learn library
execute_request = deployrclient.models.ExecuteRequest("from sklearn import svm\nfrom sklearn import datasets")
execute_response = client.execute_code(session_id,execute_request, headers)
#Report if it was a success
execute_response.success
   
#Define the untrained Support Vector Classifier (SVC) object
#and the dataset to be preloaded.
execute_request = deployrclient.models.ExecuteRequest("clf=svm.SVC()\niris=datasets.load_iris()\nnames={0:'I. setosa',1:'I. versicolor',2:'I. virginica'}")
#Now, go create the object and preload Iris Dataset in R Server
execute_response = client.execute_code(session_id,execute_request, headers)
#Report if it was a success
execute_response.success
   
#Define two rows from the Iris Dataset as a sample for scoring
workspace_object = deployrclient.models.WorkspaceObject("species_1",[7,3.2,4.7,1.4])
workspace_object_2 = deployrclient.models.WorkspaceObject("species_2",[3,2.6,3,2.5])

#Define how to train the classifier model; what to predict; what to return
execute_request = deployrclient.models.ExecuteRequest(
    "clf.fit(iris.data, iris.target)\n"+
    "result=clf.predict(species_1)\n"+
    "other_result=clf.predict(species_2)",
    [workspace_object,workspace_object_2], #Input
    ["result", "other_result"]) #Output

#Now, go train that model on the Iris Dataset in R Server
execute_response = client.execute_code(session_id,execute_request, headers)

#If successful, print name and result of each output parameter. Else, print error.
if(execute_response.success):
    for result in execute_response.output_parameters:
        print("{0}: {1}".format(result.name,result.value))
else:
    print (execute_response.error_message)

#Create a snapshot of the current session
response = client.create_snapshot(session_id, deployrclient.models.CreateSnapshotRequest("Iris Snapshot"), headers)
#Return the snapshot ID for reference when you publish later.
response.snapshot_id
#If you forget the ID, list snapshots to get the ID again.
for snapshot in client.list_snapshots(headers):
    print(snapshot)

##################################################
##        PUBLISH AS A SERVICE IN PYTHON        ##
##################################################

#Define a web service that determines the iris species by scoring 
#a vector of sepal length and width, petal length and width

#Set `flower_data` for the sepal and petal length and width
flower_data = deployrclient.models.ParameterDefinition(name = "flower_data", type = "vector")
#Set `iris_species` for the species of iris
iris_species = deployrclient.models.ParameterDefinition(name = "iris_species", type = "vector")

#Define the publish request for the web service and its arguments.
#Specify the code, inputs, outputs, and snapshot.
#Don't forget to set runtime_type="Python"`.
publish_request = deployrclient.models.PublishWebServiceRequest(
       code = "iris_species = [names[x] for x in clf.predict(flower_data)]", 
       input_parameter_definitions = [flower_data], 
       output_parameter_definitions = [iris_species],
       runtime_type = "Python",
       snapshot_id = response.snapshot_id)

#Publish the service using the specified name (iris), version (V1.0)
client.publish_web_service_version("Iris", "V1.0", publish_request, headers)

##################################################
##           CONSUME SERVICE IN PYTHON          ##
##################################################

# Inspect holdings and metadata for service Iris V1.0.
for service in client.get_web_service_version("Iris","V1.0", headers):
    #print service metadata (description, who published,...)
    print(service)
    #Print input and output parameters as defined in service definition object
    print("Input Parameters: {0}".format([str(parameter) for parameter in service.input_parameter_definitions]))
    print("Output Parameters: {0}".format([str(parameter) for parameter in service.output_parameter_definitions]))

#Import the requests library to make requests on the server
import requests
#Import the JSON library to use for pretty printing of json responses
import json

#Create a requests `Session` object.
s = requests.Session()

#Record the R Server endpoint URL hosting the web services you created before
url = "http://localhost:12800"

#Give the request.Session object the authentication headers 
#so you don't have to repeat it with each request.
s.headers = headers

#Retrieve the service-specific swagger file using the requests library.
swagger_resp = s.get(url+"/api/Iris/V1.0/swagger.json")

#Either, download service-specific swagger file using the json library.
with open('iris_swagger.json','w') as f:
   (json.dump(client.get_web_service_swagger("Iris","V1.0",headers),f, indent = 1))

#Or, print just what you need from the Swagger file, 
#such as the routing paths for the endpoints to be consumed.
print(json.dumps(swagger_resp.json()["paths"], indent = 1, sort_keys = True))

#Or, print input and output parameters as defined in the Swagger.io format
print("Input")
print(json.dumps(swagger_resp.json()["definitions"]["InputParameters"], indent = 1, sort_keys = True))
print("Output")
print(json.dumps(swagger_resp.json()["definitions"]["WebServiceResult"], indent = 1, sort_keys = True))

#Make the request to consume the service using these flower_data inputs
resp = s.post(url+"/api/Iris/V1.0",json={"flower_data":[7,3.2,4.7,1.4]})
#Print the output
print(json.dumps(resp.json(), indent = 1, sort_keys = True))

#Use input from another Iris species.
resp = s.post(url+"/api/Iris/V1.0",json={"flower_data":[3,2.6,3,2.5]})
print(json.dumps(resp.json(), indent = 1, sort_keys = True))

#Use input from another Iris species.
resp = s.post(url+"/api/Iris/V1.0",json={"flower_data":[5.1,3.5,1.4,.2]})
print(json.dumps(resp.json(), indent = 1, sort_keys = True))

##################################################
##          MANAGE SERVICES IN PYTHON           ##
##################################################

#Define what needs to be updated. Here we add a description.
#Be sure to specify the runtime_type again.
update_request = deployrclient.models.PublishWebServiceRequest(
    description = "Determines iris species using length and width of sepal and petal", runtime_type = "Python")
#Now update it by specifying the service name and version number
client.patch_web_service_version("Iris", "V1.0", update_request, headers)

#Or, publish another version of the web service, but this time 
#the service returns the species as a string instead of list of strings.
flower_data = deployrclient.models.ParameterDefinition(name = "flower_data", type = "vector")
iris_species = deployrclient.models.ParameterDefinition(name = "iris_species", type = "string")
 
#Define the publish request for the service and its arguments.
#Specify the changed code, inputs, outputs, and snapshot.
#Don't forget to set runtime_type="Python"`.
publish_request = deployrclient.models.PublishWebServiceRequest(
    code = "iris_species = [names[x] for x in clf.predict(flower_data)][0]",
    description = "Determines the species of iris, based on Sepal Length, Sepal Width, Petal Length and Petal Width",
    input_parameter_definitions = [flower_data],
    output_parameter_definitions = [iris_species],
    runtime_type = "Python",
    snapshot_id = response.snapshot_id)
 
#Now, publish the service with version (V2.0)
client.publish_web_service_version("Iris", "V2.0", publish_request, headers)
 
#Make request to consume service using these flower_data inputs; print output
resp = s.post(url+"/api/Iris/V2.0",json={"flower_data":[5.1,3.5,1.4,.2]})
print(json.dumps(resp.json(), indent = 1, sort_keys = True))

#Return the list of all existing web services.
for service in client.get_all_web_services(headers):
    #print the service information
    print(service)
    #Print each input and output parameter
    print("Input Parameters: {0}".format([str(parameter) for parameter in service.input_parameter_definitions]))
    print("Output Parameters: {0}".format([str(parameter) for parameter in service.output_parameter_definitions]))

#Delete the second version we just published.
client.delete_web_service_version("Iris","V2.0",headers)
```

## <a name="walkthrough"></a>Tutorial

Esta sección describe cómo funciona el código con más detalle.


### <a name="prereq"></a>Paso 1. Crear bibliotecas de cliente de requisitos previos

Antes de poder empezar a publicar su Python código y los modelos thorugh aprendizaje de máquina de Microsoft Server, debe generar una biblioteca de cliente con el documento de Swagger proporcionado en esta versión.

1. Instale un generador de código de Swagger en el equipo local y familiarizarse con él. Se usará para generar las bibliotecas de cliente de la API de Python. Herramientas populares incluyen [Azure AutoRest](https://github.com/Azure/autorest) (requiere Node.js) y [Swagger Codegen](https://github.com/swagger-api/swagger-codegen). 

2. Descargue el archivo Swagger que contiene el núcleo de la API para su versión de servidor de aprendizaje de máquina. Este archivo contiene una plantilla de Swagger que defina la lista de recursos de REST y las operaciones que se pueden llamar en esos recursos. Puede encontrar este archivo en `https://microsoft.github.io/deployr-api-docs/swagger/<version>/rserver-swagger-<version>.json`, donde `<version>` es el número de versión del servidor de R de 3 dígitos. 

   Por ejemplo, para R Server 9.1 se descarga de: https://microsoft.github.io/deployr-api-docs/9.1.0/swagger/rserver-swagger-9.1.0.json

3. Generar la biblioteca de cliente generada de forma estática, pasando el `rserver-swagger-<version>.json` al generador de código de Swagger de archivos y especificar el idioma que desee. En este caso, debe especificar Python.  

    Por ejemplo, si utiliza AutoRest para generar una biblioteca de cliente de Python, podría ser similar al siguiente, donde el número de 3 dígitos representa el número de versión de R Server:
    
    `AutoRest.exe -Input rserver-swagger-9.1.0.json -CodeGenerator Python  -OutputDirectory C:\Users\rserver-user\Documents\Python`

4. También puede proporcionar algunos encabezados personalizados y realizar otros cambios antes de usar al cliente generado código auxiliar de biblioteca. Consulte la [interfaz de línea de comandos](https://github.com/Azure/autorest/blob/master/docs/user/cli.md) documentación a GitHub para obtener más información sobre las distintas opciones de configuración y las preferencias, como cambiar el nombre del espacio de nombres.
   
5. Explorar la biblioteca de cliente principal para ver las distintas llamadas de API que puede realizar. 

    En nuestro ejemplo, Autorest genera algunos directorios y archivos de la biblioteca de cliente de Python en su sistema local. De forma predeterminada, son el espacio de nombres (y directorio) `deployrclient` y podría ser similar a esto:
   
   ![Ruta de acceso de salida de Autorest](./media/data-scientist-python-autorest.png)

    Para este espacio de nombres predeterminado, se llama a la propia biblioteca de cliente `deploy_rclient.py`. Si abre este archivo en el IDE, como Visual Studio, verá algo parecido a esto:
   
   ![Biblioteca de cliente de Python](./media/data-scientist-python-client-library.png)


### <a name="step-2-add-authentication-and-header-logic"></a>Paso 2. Agregar lógica de autenticación y encabezado

Tenga en cuenta que todas las API requieren autenticación; por lo tanto, todos los usuarios deben autenticarse al realizar una API llama mediante el `POST /login` API o a través de Azure Active Directory (AAD). 

Para simplificar este proceso, se emiten tokens de acceso de portador para que los usuarios no tienen que proporcionar sus credenciales para cada llamada.  Este token de portador es un token de seguridad ligero que concede acceso al "portador" a un recurso protegido: en este caso, las API del servidor de aprendizaje de máquina. Después de que se ha autenticado un usuario, la aplicación debe validar el token de portador del usuario para asegurarse de que la autenticación fue correcta para las entidades previstas. Para más información acerca de cómo administrar estos tokens, consulte [Tokens de acceso de seguridad](https://msdn.microsoft.com/microsoft-r/operationalize/security-access-tokens).

Antes de interactuar con las API principales, en primer lugar autenticar, obtener el acceso de portador símbolo (token) utilizando el [método de autenticación](https://msdn.microsoft.com/microsoft-r/operationalize/security-authentication) configurado por el administrador y, a continuación, se incluyen en cada encabezado para cada solicitud siguiente:

1. Introducción mediante la importación de la biblioteca de cliente para que sea accesible desde su Python preferido editor de código, como Jupyter, Visual Studio, el código de VS o iPython.

   Especifique el directorio principal de la biblioteca de cliente. En nuestro ejemplo, la biblioteca de cliente generado Autorest está bajo `C:\Users\rserver-user\Documents\Python\deployrclient`:

   ```python
   # Import the generated client library
   import deployrclient
   ```

2. Agregue la lógica de autenticación a la aplicación para definir una conexión desde el equipo local al servidor de aprendizaje de máquina, proporcione las credenciales, capturar el token de acceso, agregar ese token en el encabezado. A continuación, usar ese encabezado para todas las solicitudes subsiguientes.  Utilice el método de autenticación definido por el administrador: cuenta de administración básicas, / LDAP de Active Directory (AD/LDAP) o Azure Active Directory (AAD).

   **AD/LDAP o `admin` autenticación de cuentas**

   Llame a la `POST /login` API para la autenticación. Pase el `username` y `password` para el administrador local, o si Active Directory está habilitado, pasar la información de cuenta LDAP. A su vez, el servidor de aprendizaje de máquina emite un token de portador/acceso. Una vez autenticado, el usuario ya no necesita proporcionar credenciales de nuevo, siempre y cuando el token sigue siendo válido y se envía un encabezado con cada solicitud. Si no conoce la configuración de conexión, póngase en contacto con su administrador.

   ```python
   #Using client library generated from Autorest
   #Create client instance and point it at an R Server. 
   #In this case, R Server is local.
   client = deployrclient.DeployRClient("http://localhost:12800")
   
   #Define the login request and provide credentials. 
   #Update values with the connection parameters from your admin.
   login_request = deployrclient.models.LoginRequest("<<your-username>>","<<your-password>>")
   #Make a call to the /login API. 
   #Store the returned an access token in a variable.
   token_response = client.login(login_request)
   ```

   **Autenticación de Azure Active Directory (AAD)**

   Pasar las credenciales AAD, entidad y un identificador de cliente. A su vez, emite AAD el [token de acceso de portador](https://msdn.microsoft.com/microsoft-r/operationalize/security-access-tokens). Una vez autenticado, el usuario ya no necesita proporcionar credenciales de nuevo, siempre y cuando el token sigue siendo válido y se envía un encabezado con cada solicitud. Si no conoce la configuración de conexión, póngase en contacto con su administrador.

   ```python
   #Import the AAD authentication library
   import adal
   
   #Define the login request and provide credentials. 
   #Use the AAD connection parameters provided by your admin.
   url = "http://localhost:12800"
   authuri = https://login.windows.net,
   tenantid = "<<AAD_DOMAIN>>", 
   clientid = "<<NATIVE_APP_CLIENT_ID>>", 
   resource = "<<WEB_APP_CLIENT_ID>>", 
   
   #Acquire authentication token using AAD Device Code Login
   context = adal.AuthenticationContext(authuri+'/'+tenantid, api_version=None)
   code = context.acquire_user_code(resource, clientid)
   print(code['message'])
   token = context.acquire_token_with_device_code(resource, code, clientid)
   #The authentication code returned must be entered at https://aka.ms/devicelogin 
   ```     

3. Agregar la `Bearer` acceder a símbolo (token) y compruebe que el servidor de aprendizaje de máquina se está ejecutando actualmente.  Este token se devuelve durante la autenticación y **deben incluirse en cada encabezado de solicitud posterior**. Este ejemplo utiliza una biblioteca de cliente generada por Autorest.

   > [!IMPORTANT]
   > Cada llamada a la API debe autenticarse. Por lo tanto, no olvide incluir encabezados con tokens para cada solicitud.

   ```python
   #Add the returned access token to the headers variable.
   headers = {"Authorization": "Bearer {0}".format(token_response.access_token)}
   
   #Verify that the server is running.
   #Remember to include `headers` in every request!
   status_response = client.status(headers) 
   print(status_response.status_code)
   ```

### <a name="step-3-prepare-session-and-code"></a>Paso 3. Preparar la sesión y el código

Después de la autenticación, puede iniciar una sesión de Python y crear un modelo para publicar más tarde. Puede incluir cualquier código Python o modelos en un servicio web. Una vez configurado el entorno de la sesión, incluso puede guardarlo como una instantánea por lo que puede volver a cargar la sesión ya tenía con anterioridad. 

> [!IMPORTANT]
> No olvide incluir `headers` en cada solicitud.

1. Crear una sesión de Python en R Server. Asegúrese de especificar un nombre y el lenguaje de Python (`runtime_type="Python"`).  Si no establece el tipo en tiempo de ejecución para Python, el valor predeterminado es R.

   Se trata de una continuación del ejemplo de uso de la biblioteca de cliente generada por Autorest:

   ```python
   #Since already logged in, create a Python session.
   #Define session using name (`Session 1`) and `runtime_type="Python"`.
   #Remember to specify the Python runtime type.
   create_session_request = deployrclient.models.CreateSessionRequest("Session 1", runtime_type="Python")
   
   #Make the call to start the session. 
   #Remember to include headers in every method call to the server.
   #Returns a session ID.
   response = client.create_session(create_session_request, headers) 
   
   #Store the session ID in a variable called `session_id` 
   #to be able to identify it later at execution time.
   session_id = response.session_id
   ```

2. Crear o llamar a un modelo de Python que podrá publicar como un servicio web

   En este ejemplo, se entrenar un modelo de máquinas (SVM) de SciKit: Obtenga información sobre soporte técnico de vector en Iris Dataset en una instancia remota del servidor de aprendizaje de máquina.  Este conjunto de datos está disponible en la [scikit-Obtenga información acerca de sitio](http://scikit-learn.org/stable/auto_examples/datasets/plot_iris_dataset.html).

   ```python
   #Import SVM and datasets from the SciKit-Learn library
   execute_request = deployrclient.models.ExecuteRequest("from sklearn import svm\nfrom sklearn import datasets")
   execute_response = client.execute_code(session_id,execute_request, headers)
   #Report if it was a success
   execute_response.success
   
   #Define the untrained Support Vector Classifier (SVC) object
   #and the dataset to be preloaded.
   execute_request = deployrclient.models.ExecuteRequest("clf=svm.SVC()\niris=datasets.load_iris()\nnames={0:'I. setosa',1:'I. versicolor',2:'I. virginica'}")
   #Now, go create the object and preload Iris Dataset in R Server
   execute_response = client.execute_code(session_id,execute_request, headers)
   #Report if it was a success
   execute_response.success
   
   #Define two rows from the Iris Dataset as a sample for scoring
   workspace_object = deployrclient.models.WorkspaceObject("species_1",[7,3.2,4.7,1.4])
   workspace_object_2 = deployrclient.models.WorkspaceObject("species_2",[3,2.6,3,2.5])

   #Define how to train the classifier model; what to predict; what to return
   execute_request = deployrclient.models.ExecuteRequest(
       "clf.fit(iris.data, iris.target)\n"+
       "result=clf.predict(species_1)\n"+
       "other_result=clf.predict(species_2)",
       [workspace_object,workspace_object_2], #Input
       ["result", "other_result"]) #Output

   #Now, go train that model on the Iris Dataset in R Server
   execute_response = client.execute_code(session_id,execute_request, headers)

   #If successful, print name and result of each output parameter. Else, print error.
   if(execute_response.success):
       for result in execute_response.output_parameters:
           print("{0}: {1}".format(result.name,result.value))
   else:
       print (execute_response.error_message)
   ```

3. Crear una instantánea de esta Python sesión para este entorno puede guardarse en el servicio web y reproducir en consumen el tiempo. Las instantáneas son útiles cuando se necesita un entorno preparado que incluye determinadas bibliotecas, objetos, modelos, archivos y artefactos. Las instantáneas de guardar el área de trabajo completo y el directorio de trabajo. Sin embargo, al publicar, puede usar sólo las instantáneas que haya creado.

   ```python
   #Create a snapshot of the current session.
   response = client.create_snapshot(session_id, deployrclient.models.CreateSnapshotRequest("Iris Snapshot"), headers)
   
   #Return the snapshot ID for reference when you publish later.
   response.snapshot_id
   
   #If you forget the ID, list snapshots to get the ID again.
   for snapshot in client.list_snapshots(headers):
       print(snapshot)
   ```

  > [!NOTE] 
   > Aunque también se pueden usar instantáneas al publicar un servicio web para las dependencias de entorno, puede tener un impacto en el rendimiento de la hora de consumo.  Para obtener un rendimiento óptimo, considere detenidamente el tamaño de la instantánea y asegurarse de mantener sólo los objetos de área de trabajo que necesita y purga el resto. En una sesión, puede usar la versión de Python `del` función o [el `deleteWorkspaceObject` solicitud de API](https://microsoft.github.io/deployr-api-docs/#delete-workspace-object) para quitar los objetos innecesarios. 

### <a name="step-4-publish-the-model"></a>Paso 4. Publicar el modelo 

Después de que se ha generado la biblioteca de cliente y la lógica de autenticación que haya creado en la aplicación, puede interactuar con el núcleo de API para crear una sesión de Python, crear un modelo y, a continuación, publicar un servicio web mediante ese modelo.

Algunas cosas que recordar:

+ Se debe autenticar antes de realizar las llamadas a API. Por lo tanto, se incluyen `headers` en todas las solicitudes.
+ Para asegurarse de que el servicio web está registrado como un servicio de Python, no olvide especificar `runtime_type="Python"`. Si no establece el tipo en tiempo de ejecución para Python, el valor predeterminado es R.
+ Puntuación requiere un vector con longitud sepal, ancho de sepal, longitud de pétalo y ancho pétalo

El código siguiente, publica el modelo SVM como un servicio web de Python. Este servicio web genera una categoría de predicción basada en valores pasados a él.

```python
   #Set `flower_data` for the sepal and petal length and width
   flower_data = deployrclient.models.ParameterDefinition(name = "flower_data", type = "vector")
   #Set `iris_species` for the species of iris
   iris_species = deployrclient.models.ParameterDefinition(name = "iris_species", type = "vector")
   
   #Define the publish request for the web service and its arguments.
   #Specify the code, inputs, outputs, and snapshot.
   #Don't forget to set runtime_type="Python"`.
   publish_request = deployrclient.models.PublishWebServiceRequest(
       code = "iris_species = [names[x] for x in clf.predict(flower_data)]", 
       input_parameter_definitions = [flower_data], 
       output_parameter_definitions = [iris_species],
       runtime_type = "Python",
       snapshot_id = response.snapshot_id)

   #Publish the service using the specified name (iris), version (V1.0)
   client.publish_web_service_version("Iris", "V1.0", publish_request, headers)
```

### <a name="step-5-consume-the-web-service"></a>Paso 5. Consumir el servicio web

Esta sección muestra cómo utilizar el servicio en la misma sesión donde se creó.

1. En la misma sesión, obtener explotaciones de servicio y los metadatos del servicio.

   ```python
   # Inspect holdings and metadata for service Iris V1.0.
   for service in client.get_web_service_version("Iris","V1.0", headers):
       #print service metadata (description, who published,...)
       print(service)
       #Print input and output parameters as defined in service definition object
       print("Input Parameters: {0}".format([str(parameter) for parameter in service.input_parameter_definitions]))
       print("Output Parameters: {0}".format([str(parameter) for parameter in service.output_parameter_definitions]))
   ```

2. Examine las explotaciones de servicio y prepárese para consumir. 
   ```python
   #Import the requests library to make requests on the server
   import requests
   #Import the JSON library to use for pretty printing of json responses
   import json

   #Create a requests `Session` object.
   s = requests.Session()

   #Record the R Server endpoint URL hosting the web services you created
   url = "http://localhost:12800"

   #Include the request.Session object in the authentication headers.
   #By doing so, you don't need to repeat it with each request.
   s.headers = headers

   # Retrieve the service-specific Swagger file using the requests library.
   swagger_resp = s.get(url+"/api/Iris/V1.0/swagger.json")

   #You can download a service-specific Swagger file using the json library.
   with open('iris_swagger.json','w') as f:
      (json.dump(client.get_web_service_swagger("Iris","V1.0",headers),f, indent = 1))

   #Or, you can print just what you need from the Swagger file. 
   #This example gets the routing paths for the endpoints to be consumed.
   print(json.dumps(swagger_resp.json()["paths"], indent = 1, sort_keys = True))

   #You can also print input and output parameters as defined in the Swagger.io format
   print("Input")
   print(json.dumps(swagger_resp.json()["definitions"]["InputParameters"], indent = 1, sort_keys = True))
   print("Output")
   print(json.dumps(swagger_resp.json()["definitions"]["WebServiceResult"], indent = 1, sort_keys = True))
   ```

3. Utilizar el servicio proporcionando algunos entrada y obtener las especies IRI. 
   ```python
   #Make the request to consume the service using these flower_data inputs
   resp = s.post(url+"/api/Iris/V1.0",json={"flower_data":[7,3.2,4.7,1.4]})
   #Print the output
   print(json.dumps(resp.json(), indent = 1, sort_keys = True))

   ##Use input from another Iris species.
   resp = s.post(url+"/api/Iris/V1.0",json={"flower_data":[3,2.6,3,2.5]})
   print(json.dumps(resp.json(), indent = 1, sort_keys = True))

   ##Use input from another Iris species.
   resp = s.post(url+"/api/Iris/V1.0",json={"flower_data":[5.1,3.5,1.4,.2]})
   print(json.dumps(resp.json(), indent = 1, sort_keys = True))
   ```

## <a name="managing-the-services"></a>Administrar los servicios

Ahora que ha creado un servicio web, puede actualizar, eliminar o volver a publicar ese servicio. También puede enumerar todos los servicios web que se hospedan mediante R Server (o servidor de aprendizaje de máquina).

### <a name="update-a-web-service"></a>Actualizar un servicio web

 En este ejemplo, se actualice el servicio para agregar una descripción útil para las personas que pueden consumir este servicio.

```python
#Define what needs to be updated. Here we add a description.
#Be sure to specify the runtime_type again.
update_request = deployrclient.models.PublishWebServiceRequest(
    description = "Determines iris species using length and width of sepal and petal", runtime_type = "Python")
#Now update it by specifying the service name and version number
client.patch_web_service_version("Iris", "V1.0", update_request, headers)
```

Puede actualizar un servicio web para cambiar el código, modelo, descripción, entradas, salidas y mucho más.

### <a name="publish-another-version"></a>Otra versión de publicación

En este ejemplo, el servicio devolverá ahora las especies IRI como una cadena en lugar de como una lista de cadenas.

```python
#Publish another version of the web service, but this time 
#the service returns the species as a string instead of list of strings.
flower_data = deployrclient.models.ParameterDefinition(name = "flower_data", type = "vector")
iris_species = deployrclient.models.ParameterDefinition(name = "iris_species", type = "string")
 
#Define the publish request for the service and its arguments.
#Specify the changed code, inputs, outputs, and snapshot.
#Don't forget to set runtime_type="Python"`.
publish_request = deployrclient.models.PublishWebServiceRequest(
    code = "iris_species = [names[x] for x in clf.predict(flower_data)][0]",
    description = "Determines the species of iris, based on Sepal Length, Sepal Width, Petal Length and Petal Width",
    input_parameter_definitions = [flower_data],
    output_parameter_definitions = [iris_species],
    runtime_type = "Python",
    snapshot_id = response.snapshot_id)
 
#Now, publish the service with version (V2.0)
client.publish_web_service_version("Iris", "V2.0", publish_request, headers)
 
#Make request to consume service using these flower_data inputs; print output
resp = s.post(url+"/api/Iris/V2.0",json={"flower_data":[5.1,3.5,1.4,.2]})
print(json.dumps(resp.json(), indent = 1, sort_keys = True))
```

Puede usar este patrón para publicar varias versiones del mismo servicio web. 

### <a name="list-services"></a>Lista de servicios

En este ejemplo se obtiene una lista de todos los servicios web, las creadas por otros usuarios o en otros idiomas incluidas.

```python
#Return the list of all existing web services.
for service in client.get_all_web_services(headers):
    #print the service information
    print(service)
    #Print each input and output parameter
    print("Input Parameters: {0}".format([str(parameter) for parameter in service.input_parameter_definitions]))
    print("Output Parameters: {0}".format([str(parameter) for parameter in service.output_parameter_definitions]))
``` 

### <a name="delete-services"></a>Eliminar servicios

En este ejemplo, eliminamos la segunda versión de servicio web que acaba de publicar.

```python
#Delete the second version we just published.
client.delete_web_service_version("Iris","V2.0",headers)
```

Puede eliminar cualquier servicio que ha creado. Puede eliminar los servicios de otros usuarios sólo si se le asigna a un rol que tiene los permisos adecuados.