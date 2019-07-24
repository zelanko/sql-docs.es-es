---
title: Consumo de aplicaciones en clústeres de macrodatos
titleSuffix: SQL Server big data clusters
description: Consuma una aplicación implementada en SQL Server clúster de macrodatos de 2019 con un servicio web RESTful (versión preliminar).
author: jeroenterheerdt
ms.author: jterh
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: a2135ef64fb17eba62eab75b81739eda047167ab
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419509"
---
# <a name="consume-an-app-deployed-on-sql-server-big-data-cluster-using-a-restful-web-service"></a>Uso de una aplicación implementada en SQL Server clúster de Big Data mediante un servicio web RESTful

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este artículo se describe cómo consumir una aplicación implementada en un clúster de macrodatos SQL Server 2019 con un servicio web RESTful (versión preliminar).

## <a name="prerequisites"></a>Requisitos previos

- [Clúster de macrodatos de SQL Server 2019](deployment-guidance.md)
- [utilidad de línea de comandos mssqlctl](deploy-install-azdata.md)
- Una aplicación implementada mediante [azdata](big-data-cluster-create-apps.md) o la [extensión de implementación](app-deployment-extension.md) de la aplicación

## <a name="capabilities"></a>Capabilities

Después de haber implementado una aplicación en el clúster SQL Server 2019 Big Data (versión preliminar), puede obtener acceso a esa aplicación y utilizarla con un servicio web RESTful. Esto permite la integración de esa aplicación desde otras aplicaciones o servicios (por ejemplo, una aplicación móvil o un sitio web). En la tabla siguiente se describen los comandos de implementación de aplicaciones que puede usar con **azdata** para obtener información sobre el servicio web RESTful de la aplicación.

|Comando |Descripción |
|:---|:---|
|`azdata app describe` | Describir aplicación. |

Puede obtener ayuda con el `--help` parámetro, como en el ejemplo siguiente:

```bash
azdata app describe --help
```

En las secciones siguientes se describe cómo recuperar un punto de conexión para una aplicación y cómo trabajar con el servicio web RESTful para la integración de aplicaciones.

## <a name="retrieve-the-endpoint"></a>Recuperación del punto de conexión

El comando Descripción de la **aplicación azdata** proporciona información detallada sobre la aplicación, incluido el punto final del clúster. Normalmente, lo usa un desarrollador de aplicaciones para compilar una aplicación con el cliente de Swagger y usar el servicio WebService para interactuar con la aplicación de una manera de RESTful.

Describa la aplicación mediante la ejecución de un comando similar al siguiente:

```bash
azdata app describe --name addpy --version v1
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
    "app": "https://10.1.1.3:30777/api/app/addpy/v1",
    "swagger": "https://10.1.1.3:30777/api/app/addpy/v1/swagger.json"
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

Anote la dirección IP (`10.1.1.3` en este ejemplo) y el número de puerto`30777`() en la salida.

## <a name="generate-a-jwt-access-token"></a>Generar un token de acceso de JWT

Para tener acceso al servicio web RESTful de la aplicación que ha implementado primero debe generar un token de acceso de JWT. Abra la siguiente dirección URL en el explorador `https://[IP]:[PORT]/api/docs/swagger.json` : mediante la dirección IP y el puerto que recuperó al ejecutar el `describe` comando anterior. Tendrá que iniciar sesión con las mismas credenciales que usó para `azdata login`.

Pegue el contenido de `swagger.json` en el editor de [Swagger](https://editor.swagger.io) para comprender qué métodos están disponibles:

![Swagger de API](media/big-data-cluster-consume-apps/api_swagger.png)

Observe el `app` método get y el `token` método post. Dado que la autenticación para las aplicaciones usa tokens JWT, tendrá que obtener un token My mediante su herramienta favorita para realizar una llamada post al `token` método. Este es un ejemplo de cómo hacer justamente eso en [Postman](https://www.getpostman.com/):

![Token de Postman](media/big-data-cluster-consume-apps/postman_token.png)

El resultado de esta solicitud le proporcionará un JWT `access_token`, que tendrá que llamar a la dirección URL para ejecutar la aplicación.

## <a name="execute-the-app-using-the-restful-web-service"></a>Ejecución de la aplicación mediante el servicio web RESTful

> [!NOTE]
> Si lo desea, puede abrir la dirección URL `swagger` del que se devolvió cuando se ejecutó `azdata app describe --name [appname] --version [version]` en el explorador, que debe ser similar `https://[IP]:[PORT]/api/app/[appname]/[version]/swagger.json`a. Tendrá que iniciar sesión con las mismas credenciales que usó para `azdata login`. Contenido del `swagger.json` que puede pegar en el [Editor de Swagger](https://editor.swagger.io). Verá que el servicio Web expone el `run` método. Fíjese también en la dirección URL base que se muestra en la parte superior.

Puede usar su herramienta favorita para llamar al `run` método (`https://[IP]:30778/api/app/[appname]/[version]/run`), pasando los parámetros en el cuerpo de la solicitud post como JSON. En este ejemplo, usaremos [Postman](https://www.getpostman.com/). Antes de hacer la llamada, debe establecer `Authorization` en `Bearer Token` y pegar en el token que recuperó anteriormente. Esto establecerá un encabezado en la solicitud. Vea la captura de pantalla siguiente.

![Encabezados de ejecución de Postman](media/big-data-cluster-consume-apps/postman_run_1.png)

Después, en el cuerpo de las solicitudes, pase los parámetros a la aplicación a la que llama y `content-type` establezca `application/json`en:

![Cuerpo de la ejecución de Postman](media/big-data-cluster-consume-apps/postman_run_2.png)

Cuando envíe la solicitud, obtendrá el mismo resultado que cuando ejecutó la aplicación mediante `azdata app run`:

![Resultado de la ejecución de Postman](media/big-data-cluster-consume-apps/postman_result.png)

Ahora se ha llamado correctamente a la aplicación a través del servicio Web. Puede seguir pasos similares para integrar este servicio Web en la aplicación.

## <a name="next-steps"></a>Pasos siguientes

También puede consultar los ejemplos adicionales en [ejemplos de implementación de aplicaciones](https://aka.ms/sql-app-deploy).

Para más información sobre los clústeres de macrodatos de SQL Server, consulte [¿Qué son los clústeres de macrodatos de SQL Server 2019?](big-data-cluster-overview.md).
