---
title: Consumo de aplicaciones
titleSuffix: SQL Server Big Data Clusters
description: Consuma una aplicación implementada en clústeres de macrodatos de SQL Server con un servicio web RESTful.
author: jeroenterheerdt
ms.author: jterh
ms.reviewer: mikeray
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 32b3884b48e20b73da186f8c0d80e6c85516a8ed
ms.sourcegitcommit: b4ad3182aa99f9cbfd15f4c3f910317d6128a2e5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/06/2019
ms.locfileid: "73707176"
---
# <a name="consume-an-app-deployed-on-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd-using-a-restful-web-service"></a>Consumo de una aplicación implementada en [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] con un servicio web RESTful

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este artículo se explica cómo consumir una aplicación implementada en un clúster de macrodatos de SQL Server con un servicio web RESTful.

## <a name="prerequisites"></a>Prerequisites

- [Clúster de macrodatos de SQL Server](deployment-guidance.md)
- [Utilidad de línea de comandos azdata](deploy-install-azdata.md)
- Una aplicación implementada mediante [azdata](big-data-cluster-create-apps.md) o la [extensión de implementación de aplicaciones](app-deployment-extension.md)

## <a name="capabilities"></a>Capabilities

Después de haber implementado una aplicación en el [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)], puede acceder a esa aplicación y consumirla mediante un servicio web RESTful. Esto permite la integración de esa aplicación desde otras aplicaciones o servicios (por ejemplo, una aplicación móvil o un sitio web). En la tabla siguiente se describen los comandos de implementación de aplicaciones que se pueden usar con **azdata** para obtener información sobre el servicio web RESTful de la aplicación.

|Comando |Descripción |
|:---|:---|
|`azdata app describe` | Describe la aplicación. |

Puede obtener ayuda con el parámetro `--help`, como en el ejemplo siguiente:

```bash
azdata app describe --help
```

En las secciones siguientes se explica cómo recuperar un punto de conexión de una aplicación y cómo trabajar con el servicio web RESTful para la integración de aplicaciones.

## <a name="retrieve-the-endpoint"></a>Recuperación del punto de conexión

El comando **azdata app describe** proporciona información detallada sobre la aplicación, incluido el punto final del clúster. Lo suelen usar los desarrolladores de aplicaciones para compilar una aplicación con el cliente de Swagger y con el servicio web para interactuar con la aplicación de manera RESTful.

Describa la aplicación al ejecutar un comando similar al siguiente ejemplo:

```bash
azdata app describe --name add-app --version v1
```

```json
{
  "input_param_defs": [
    {
      "name": "x",
      "type": "int"
    },
    {
      "name": "y",
      "type": "int"
    }
  ],
  "links": {
    "app": "https://10.1.1.3:30080/app/addpy/v1",
    "swagger": "https://10.1.1.3:30080/app/addpy/v1/swagger.json"
  },
  "name": "add-app",
  "output_param_defs": [
    {
      "name": "result",
      "type": "int"
    }
  ],
  "state": "Ready",
  "version": "v1"
}
```

Anote la dirección IP (`10.1.1.3` en este ejemplo) y el número de puerto (`30080`) de la salida.

Otra de las diversas formas de obtener esta información es haciendo clic con el botón derecho en Administrar en el servidor de Azure Data Studio, donde encontrará los puntos de conexión de los servicios enumerados.

![Punto de conexión de ADS](media/big-data-cluster-consume-apps/ads_end_point.png)

## <a name="generate-a-jwt-access-token"></a>Generar un token de acceso JWT

Para acceder al servicio web RESTful de la aplicación que ha implementado, primero debe generar un token de acceso JWT. Abra la siguiente dirección URL en el explorador: `https://[IP]:[PORT]/docs/swagger.json` con la dirección IP y el puerto que ha recuperado al ejecutar el comando `describe` arriba. Tiene que iniciar sesión con las mismas credenciales que ha usado para `azdata login`.

Pegue el contenido de `swagger.json` en el [editor de Swagger](https://editor.swagger.io) para conocer qué métodos están disponibles:

![API de Swagger](media/big-data-cluster-consume-apps/api_swagger.png)

Observe el método GET `app` y el método POST `token`. Dado que la autenticación de aplicaciones usa tokens JWT, necesita obtener un token mediante su herramienta favorita para realizar una llamada POST al método `token`. Este es un ejemplo de cómo hacer justamente eso en [Postman](https://www.getpostman.com/):

![Token de Postman](media/big-data-cluster-consume-apps/postman_token.png)

El resultado de esta solicitud proporciona un `access_token` JWT, necesario para llamar a la dirección URL a fin de ejecutar la aplicación.

## <a name="execute-the-app-using-the-restful-web-service"></a>Ejecutar la aplicación mediante el servicio web RESTful

> [!NOTE]
> Si quiere, puede abrir la dirección URL de `swagger` devuelta al ejecutar `azdata app describe --name [appname] --version [version]` en el explorador, que debe ser similar a `https://[IP]:[PORT]/app/[appname]/[version]/swagger.json`. Tiene que iniciar sesión con las mismas credenciales que ha usado para `azdata login`. Puede pegar el contenido de `swagger.json` en el [editor de Swagger](https://editor.swagger.io). Se ve que el servicio web expone el método `run`. Además, observe la dirección URL base que se muestra en la parte superior.

Puede usar su herramienta favorita para llamar al método `run` (`https://[IP]:30778/api/app/[appname]/[version]/run`), pasando los parámetros del cuerpo de la solicitud POST como json. En este ejemplo se usa [Postman](https://www.getpostman.com/). Antes de realizar la llamada, debe establecer `Authorization` en `Bearer Token` y pegar el token recuperado anteriormente. Esto establece un encabezado en la solicitud. Vea la captura de pantalla siguiente.

![Encabezados de ejecución de Postman](media/big-data-cluster-consume-apps/postman_run_1.png)

Después, en el cuerpo de las solicitudes, pase los parámetros a la aplicación a la que llama y establezca `content-type` en `application/json`:

![Cuerpo de ejecución de Postman](media/big-data-cluster-consume-apps/postman_run_2.png)

Cuando envía la solicitud, obtiene el mismo resultado que cuando ejecuta la aplicación mediante `azdata app run`:

![Resultado de ejecución de Postman](media/big-data-cluster-consume-apps/postman_result.png)

Ahora ha llamado correctamente a la aplicación a través del servicio web. Puede seguir pasos similares para integrar este servicio web en la aplicación.

## <a name="next-steps"></a>Pasos siguientes

También puede ver otros ejemplos en [Ejemplos de implementación de aplicaciones](https://aka.ms/sql-app-deploy).

Vea [¿Qué son los [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md) para obtener más información sobre los [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)].
