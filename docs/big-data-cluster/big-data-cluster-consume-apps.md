---
title: Consumir las aplicaciones en clústeres de macrodatos
titleSuffix: SQL Server big data clusters
description: Consumir una aplicación implementada en un clúster de macrodatos de 2019 de SQL Server mediante un servicio web RESTful (versión preliminar).
author: jeroenterheerdt
ms.author: jterh
ms.reviewer: mikeray
ms.date: 03/18/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 919ffb2cd4916451245f29c7d783ca05dbfa6998
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67958883"
---
# <a name="consume-an-app-deployed-on-sql-server-big-data-cluster-using-a-restful-web-service"></a>Consumo de una aplicación implementada en el clúster de macrodatos de SQL Server mediante un servicio web RESTful

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este artículo se describe cómo consumir una aplicación implementada en un clúster de macrodatos de 2019 de SQL Server mediante un servicio web RESTful (versión preliminar).

## <a name="prerequisites"></a>Requisitos previos

- [Clúster de macrodatos de SQL Server 2019](deployment-guidance.md)
- [utilidad de línea de comandos mssqlctl](deploy-install-mssqlctl.md)
- Una aplicación implementada mediante [ `mssqlctl` ](big-data-cluster-create-apps.md) o [implementar aplicación de extensión](app-deployment-extension.md)

## <a name="capabilities"></a>Capabilities

Después de haber implementado una aplicación en el clúster de macrodatos de 2019 de SQL Server (versión preliminar), puede acceder y usar esa aplicación mediante un servicio web RESTful. Esto permite la integración de esa aplicación desde otras aplicaciones o servicios (por ejemplo, una aplicación móvil o un sitio Web). En la tabla siguiente se describe los comandos de implementación de aplicación que puede usar con **mssqlctl** para obtener información sobre el servicio web de RESTful para la aplicación.

|Comando |Descripción |
|:---|:---|
|`mssqlctl app describe` | Describir la aplicación. |

También puede obtener ayuda con la `--help` parámetro como en el ejemplo siguiente:

```bash
mssqlctl app describe --help
```

Las secciones siguientes describen cómo recuperar un punto de conexión para una aplicación y cómo trabajar con el servicio web RESTful para la integración de aplicaciones.

## <a name="retrieve-the-endpoint"></a>Recuperar el punto de conexión

El **mssqlctl aplicación describen** comando proporciona información detallada acerca de la aplicación, incluido el punto final en el clúster. Esto se usa normalmente por un desarrollador de aplicaciones para compilar una aplicación mediante el cliente de swagger y usar el servicio Web para interactuar con la aplicación de forma RESTful.

Describe la aplicación mediante la ejecución de un comando similar al siguiente:

```bash
mssqlctl app describe --name addpy --version v1
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

Tenga en cuenta la dirección IP (`10.1.1.3` en este ejemplo) y el número de puerto (`30777`) en la salida.

## <a name="generate-a-jwt-access-token"></a>Generar un token de acceso JWT

Para tener acceso al servicio web de RESTful para la aplicación que haya implementado primero debe generar un token de acceso de JWT. Abra la siguiente dirección URL en el explorador: `https://[IP]:[PORT]/api/docs/swagger.json` utilizando la dirección IP y puerto que recuperó en funcionamiento el `describe` comando anterior. Tendrá que iniciar sesión con las mismas credenciales que usó para `mssqlctl login`.

Pegue el contenido de la `swagger.json` en el [Swagger Editor](https://editor.swagger.io) a entender qué métodos están disponibles:

![Swagger de API](media/big-data-cluster-consume-apps/api_swagger.png)

Tenga en cuenta la `app` método GET, así como la `token` método POST. Puesto que la autenticación para las aplicaciones usa los tokens JWT deberá obtener un token de mi utilizando su herramienta favorita para realizar una llamada POST a la `token` método. Este es un ejemplo de cómo hacer exactamente eso [Postman](https://www.getpostman.com/):

![Token de postman](media/big-data-cluster-consume-apps/postman_token.png)

El resultado de esta solicitud dará un JWT `access_token`, lo que necesita llamar a la dirección URL para ejecutar la aplicación.

## <a name="execute-the-app-using-the-restful-web-service"></a>Ejecutar la aplicación mediante el servicio web RESTful

> [!NOTE]
> Si lo desea, puede abrir la dirección URL para el `swagger` que se devolvió cuando se ejecutaron `mssqlctl app describe --name [appname] --version [version]` en el explorador, lo que debe ser similar a `https://[IP]:[PORT]/api/app/[appname]/[version]/swagger.json`. Tendrá que iniciar sesión con las mismas credenciales que usó para `mssqlctl login`. El contenido de la `swagger.json` puede pegar en [Swagger Editor](https://editor.swagger.io). Verá que el servicio web expone el `run` método. Tenga en cuenta también la URL Base que se muestra en la parte superior.

Puede usar su herramienta favorita para llamar a la `run` método (`https://[IP]:30778/api/app/[appname]/[version]/run`), pasando los parámetros en el cuerpo de la solicitud POST como json. En este ejemplo usaremos [Postman](https://www.getpostman.com/). Antes de realizar la llamada, deberá establecer el `Authorization` a `Bearer Token` y pegue en el token que recuperó anteriormente. Esto establecerá un encabezado en la solicitud. Consulte la captura de pantalla siguiente.

![Postman ejecutar encabezados](media/big-data-cluster-consume-apps/postman_run_1.png)

A continuación, en el cuerpo de las solicitudes, pasar los parámetros a la aplicación que está llamando y establezca el `content-type` a `application/json`:

![Postman ejecutar cuerpo](media/big-data-cluster-consume-apps/postman_run_2.png)

Cuando se envía la solicitud, obtendrá el mismo resultado como hizo cuando ejecutó la aplicación a través de `mssqlctl app run`:

![Resultado de la ejecución de postman](media/big-data-cluster-consume-apps/postman_result.png)

Ahora se ha llamado correctamente la aplicación a través del servicio web. Puede seguir pasos similares para integrar este servicio web en la aplicación.

## <a name="next-steps"></a>Pasos siguientes

También puede consultar ejemplos adicionales en [ejemplos de implementación de aplicaciones](https://aka.ms/sql-app-deploy).

Para obtener más información acerca de los clústeres de macrodatos de SQL Server, vea [¿cuáles son los clústeres de SQL Server 2019 macrodatos?](big-data-cluster-overview.md).
