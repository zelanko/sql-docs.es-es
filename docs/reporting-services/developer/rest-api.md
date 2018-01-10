---
title: Desarrollo con las API de REST para Reporting Services| Microsoft Docs
ms.description: The REST API provides programmatic access to the objects in a SQL Server 2017 Reporting Services report server catalog.
ms.date: 10/19/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: developer
ms.reviewer: 
ms.suite: pro-bi
ms.custom: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 304d2e2c00703f98dd894e1a2d3e4688d87822f2
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/09/2018
---
# <a name="develop-with-the-rest-apis-for-reporting-services"></a>Desarrollo con las API de REST para Reporting Services

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2017-and-later](../../includes/ssrs-appliesto-2017-and-later.md)] [!INCLUDE [ssrs-appliesto-not-pbirs](../../includes/ssrs-appliesto-not-pbirs.md)]

Microsoft SQL Server 2017 Reporting Services admite las API de transferencia de estado representacional (REST). Las API de REST son puntos de conexión de servicio que admiten una serie de operaciones HTTP (métodos), que proporcionan acceso de creación, recuperación, actualización o eliminación para los recursos de un servidor de informes.

La API de REST proporciona acceso mediante programación a los objetos de un catálogo del servidor de informes de SQL Server 2017 Reporting Services. Como ejemplos de objetos tenemos las carpetas, los informes, los KPI, los orígenes de datos, los conjuntos de datos, los planes de actualización, las suscripciones, etc. Con la API de REST puede, por ejemplo, navegar por la jerarquía de carpetas, detectar el contenido de una carpeta o descargar una definición de informe. También puede crear, actualizar y eliminar objetos. Como ejemplos de acciones de trabajo con los objetos tenemos la carga de un informe, la ejecución de un plan de actualización, la eliminación de una carpeta, etc.

## <a name="components-of-a-rest-api-requestresponse"></a>Componentes de una solicitud/respuesta de la API de REST

Un par de solicitud/respuesta de una API de REST puede dividirse en cinco componentes:

* El **URI de la solicitud**, que consta de: `{URI-scheme} :// {URI-host} / {resource-path} ? {query-string}`. Aunque el URI de solicitud se incluye en el encabezado del mensaje de solicitud, aquí lo mencionamos por separado porque la mayoría de los lenguajes o marcos de trabajo le exigen que lo pase por separado desde el mensaje de solicitud.

    * Esquema de URI: indica el protocolo usado para transmitir la solicitud. Por ejemplo, `http` o `https`.
    * Host de URI: especifica el nombre de dominio o la dirección IP del servidor donde se hospeda el punto de conexión de servicio REST, como `myserver.contoso.com`.
    * Ruta de acceso del recurso: especifica el recurso o una colección de recursos, que puede incluir varios segmentos usados por el servicio a la hora de determinar la selección de esos recursos. Por ejemplo: `CatalogItems(01234567-89ab-cdef-0123-456789abcdef)/Properties` se puede usar para obtener las propiedades especificadas de CatalogItem.
    * (Opcional) Cadena de consulta: proporciona más parámetros simples, como los criterios de selección de recursos o la versión de la API.

* Campos de encabezado de mensaje de solicitud HTTP:

    * [Método HTTP](https://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html) obligatorio (también denominado " operación" o "verbo"), que indica al servicio qué tipo de operación se está solicitando. Las API de REST de Reporting Services admiten los métodos DELETE, GET, HEAD, PUT, POST y PATCH.
    * Campos de encabezado adicionales y opcionales, según necesite el método HTTP y el URI especificados.

* Campos de **cuerpo de mensaje de solicitudes** HTTP opcionales para admitir la operación HTTP y el URI. Por ejemplo, las operaciones POST contienen objetos codificados con MIME que se pasan como parámetros complejos. Para las operaciones POST o PUT, el tipo de codificación MIME para el cuerpo también debe especificarse en el encabezado de solicitud `Content-type`. Algunos servicios requieren que se use un tipo MIME concreto, como `application/json`.

* Campos de **encabezado de mensaje de respuesta HTTP**:

    * Un [código de estado HTTP](http://www.w3.org/Protocols/HTTP/HTRESP.html), que puede ser 2xx para los códigos correctos y 4xx o 5xx para los códigos de error. Como alternativa se puede devolver un código de estado definido por el servicio, como se indica en la documentación de la API.
    * Campos de encabezado adicionales y opcionales, según sea necesario para admitir la respuesta a la solicitud, como un encabezado de respuesta `Content-type`.

* Campos de **cuerpo del mensaje de respuesta** HTTP opcionales:

    * Se devuelven objetos de respuesta codificados con MIME en el cuerpo de respuesta HTTP, como una respuesta de un método GET que devuelve datos. Normalmente, estos objetos se devuelven en un formato estructurado como JSON o XML, tal y como se indica en el encabezado de respuesta `Content-type`.

## <a name="api-documentation"></a>Documentación de la API

Una API de REST moderna exige una documentación de API moderna. La API de REST se basa en la especificación de OpenAPI (también denominada "especificación de Swagger") y la documentación está disponible en [SwaggerHub](https://app.swaggerhub.com/api/microsoft-rs/SSRS/2.0). Además de documentar la API, SwaggerHub permite generar una biblioteca cliente en el lenguaje que quiera: JavaScript, TypeScript, C#, Java, Python, Ruby, etc.

## <a name="testing-api-calls"></a>Probar las llamadas API

Una herramienta para probar los mensajes de solicitud/respuesta HTTP es [Fiddler](http://www.telerik.com/fiddler). Fiddler es un proxy de depuración web gratuito que puede interceptar las solicitudes REST, lo que facilita el diagnóstico de los mensajes de solicitud/respuesta HTTP.

## <a name="next-steps"></a>Pasos siguientes

Revise las API disponibles en [SwaggerHub](https://app.swaggerhub.com/api/microsoft-rs/SSRS/2.0).

Los ejemplos están disponibles en [GitHub](https://github.com/Microsoft/Reporting-Services). El ejemplo incluye una aplicación HTML5 compilada en TypeScript, React y webpack, junto con un ejemplo de PowerShell.

¿Tiene alguna pregunta más? [Puede plantear sus dudas en el foro de Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231).
