---
title: Desarrollar con las API de REST para Reporting Services | Documentos de Microsoft
ms.description: The REST API provides programmatic access to the objects in a SQL Server 2017 Reporting Services report server catalog.
ms.date: 10/19/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: e20b96e38f798c19a74d5f3a32a25e429dc8ebeb
ms.openlocfilehash: 7c2c34047ac316045387b036cf10ee149175580a
ms.contentlocale: es-es
ms.lasthandoff: 10/20/2017

---
# <a name="develop-with-the-rest-apis-for-reporting-services"></a>Desarrollar con las API de REST para Reporting Services

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2017-and-later](../../includes/ssrs-appliesto-2017-and-later.md)] [!INCLUDE [ssrs-appliesto-not-pbirs](../../includes/ssrs-appliesto-not-pbirs.md)]

Microsoft SQL Server de 2017 Reporting Services admite Representational State Transfer (REST) API. Las API de REST son puntos de conexión de servicio que compatibilidad con un conjunto de operaciones de HTTP (métodos), logrando así crear, recuperar, actualizar o eliminar el acceso para los recursos dentro de un servidor de informes.

La API de REST proporciona acceso mediante programación a los objetos en un catálogo del servidor de informes de Reporting Services de SQL Server de 2017. Ejemplos de objetos son carpetas, informes, KPI, orígenes de datos, conjuntos de datos, planes de actualización, suscripciones y mucho más. Con la API de REST, puede, por ejemplo, navegar por la jerarquía de carpetas, detectar el contenido de una carpeta o descargar una definición de informe. También puede crear, actualizar y eliminar los objetos. Ejemplos de cómo trabajar con objetos se cargue un informe, ejecutar un plan de actualización, eliminar una carpeta y así sucesivamente.

## <a name="components-of-a-rest-api-requestresponse"></a>Componentes de una solicitud/respuesta de la API de REST

Un par de solicitud/respuesta de la API de REST puede dividirse en cinco componentes:

* El **URI de solicitud**, que consta de: `{URI-scheme} :// {URI-host} / {resource-path} ? {query-string}`. Aunque el URI de solicitud se incluye en el encabezado del mensaje de solicitud, lo llamamos aquí por separado porque la mayoría de los idiomas o marcos de trabajo debe pasarla por separado desde el mensaje de solicitud.

    * Esquema de URI: indica el protocolo utilizado para transmitir la solicitud. Por ejemplo, `http` o `https`.
    * Host del URI: especifica el nombre de dominio o la dirección IP del servidor donde se hospeda el punto de conexión de servicio REST, como `myserver.contoso.com`.
    * Ruta de acceso de recursos: especifica el recurso o una colección de recursos, que puede incluir varios segmentos utilizados por el servicio para determinar la selección de esos recursos. Por ejemplo: `CatalogItems(01234567-89ab-cdef-0123-456789abcdef)/Properties` puede utilizarse para obtener las propiedades especificadas para el CatalogItem.
    * (Opcional) de la cadena de consulta: proporciona los parámetros simples adicionales, como los criterios de selección de versión o un recurso de API.

* Campos de encabezado de mensaje de solicitud HTTP:

    * Obligatoria [método HTTP](https://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html) (también conocido como una operación o verbo), que indica al servicio qué tipo de operación que está solicitando. Informar de las API de REST de servicios compatible con DELETE, GET, HEAD, PUT, POST y aplicar revisiones a métodos.
    * Campos de encabezado adicional opcional, según sea necesario mediante el método HTTP y el URI especificado.

* HTTP opcional **cuerpo del mensaje de solicitud** campos para admitir la operación de URI y HTTP. Por ejemplo, operaciones POST contienen objetos codificado con MIME que se pasan como parámetros complejos. Para las operaciones POST o PUT, el tipo de codificación MIME para el cuerpo debe especificarse en el `Content-type` así el encabezado de solicitud. Algunos servicios requieren que se use un tipo MIME concreto, como `application/json`.

* HTTP **encabezado del mensaje de respuesta** campos:

    * Un [código de estado HTTP](http://www.w3.org/Protocols/HTTP/HTRESP.html), intervalo de códigos de éxito 2xx 4xx o 5xx códigos de error. Como alternativa, un código de estado definido por el servicio puede devolver, como se indica en la documentación de API.
    * Campos de encabezado adicional opcional, según sea necesario para admitir la respuesta a la solicitud, como un `Content-type` encabezado de respuesta.

* HTTP opcional **cuerpo del mensaje de respuesta** campos:

    * Se devuelven los objetos de respuesta codificado con MIME en el cuerpo de respuesta HTTP, como una respuesta de un método GET que devuelve datos. Normalmente, estos objetos se devuelven en un formato estructurado como JSON o XML, tal y como indica la `Content-type` encabezado de respuesta.

## <a name="api-documentation"></a>Documentación de la API

Llama a una API de REST modernos para obtener documentación API moderna. La API de REST se basa en la especificación de OpenAPI (conocido como) la especificación de swagger) y la documentación está disponible en [SwaggerHub](https://app.swaggerhub.com/api/microsoft-rs/SSRS/2.0). Más allá de la documentación de la API SwaggerHub le ayuda a generar una biblioteca de cliente en el idioma que elija: JavaScript, TypeScript, C#, Java, Python, Ruby y mucho más.

## <a name="testing-api-calls"></a>Llamadas a la API de pruebas

Es una herramienta para probar los mensajes de solicitud/respuesta HTTP [Fiddler](http://www.telerik.com/fiddler). Fiddler es un proxy que puede interceptar las solicitudes REST, lo que facilita a diagnosticar la solicitud HTTP de depuración de web gratuita / mensajes de respuesta.

## <a name="next-steps"></a>Pasos siguientes

Revise las API disponibles a través de [SwaggerHub](https://app.swaggerhub.com/api/microsoft-rs/SSRS/2.0).

Los ejemplos están disponibles en [GitHub](https://github.com/Microsoft/Reporting-Services). El ejemplo incluye una aplicación HTML5 compilada en TypeScript y reaccionar, webpack junto con un ejemplo de PowerShell.

¿Tiene alguna pregunta más? [Puede plantear sus dudas en el foro de Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231).
