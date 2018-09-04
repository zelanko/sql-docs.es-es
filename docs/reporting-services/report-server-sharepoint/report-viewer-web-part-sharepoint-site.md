---
title: 'Elemento web Visor de informes en un sitio de SharePoint: SSRS| Microsoft Docs'
ms.date: 09/25/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-server-sharepoint
ms.suite: pro-bi
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 0a754b1e77fd1b65b88664b96b0fed0f7dbdd250
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/30/2018
ms.locfileid: "43275237"
---
# <a name="report-viewer-web-part-on-a-sharepoint-site---reporting-services"></a>Elemento web Visor de informes en un sitio de SharePoint: Reporting Services

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

El elemento web Visor de informes es un elemento web personalizado. Puede usar el elemento web para ver, explorar, imprimir y exportar informes en un servidor de informes de un sitio de SharePoint. El elemento web Visor de informes está asociado a archivos de definición de informe (.rdl) que procesa el servidor de informes de Microsoft SQL Server Reporting Services. 

El elemento web Visor de informes más reciente también puede servir informes paginados implementados en Power BI Report Server. El elemento web no funciona con informes de Power BI.

## <a name="why-the-report-viewer-web-part-is-re-introduced"></a>Por qué se ha vuelto a publicar el elemento web Visor de informes

El elemento web Visor de informes estaba disponible como parte del complemento Reporting Services para productos de SharePoint. El elemento web era específico para servidores de informes en modo integrado de SharePoint. El modo integrado de SharePoint está en desuso a partir de SQL Server 2016.

A partir de SQL Server 2017, hay solo un modo de instalación de Reporting Services: **modo nativo**. Puede insertar todos los tipos de informes mediante un elemento web Visor de páginas mediante el parámetro URL *rs:Embed=true*. La inserción de informes en páginas de SharePoint es un caso de integración solicitado por los clientes y el elemento web Visor de informes actualizado permite este escenario para informes paginados.

Mientras que el elemento web Visor de páginas basta para insertar un informe paginado en una página de SharePoint, el elemento web Visor de informes actualizado ofrece características adicionales.

* Mostrar u ocultar botones concretos de barra de herramientas
* Reemplazar valores de parámetros de informe
* Conectar elementos web Filtro con parámetros de informe

## <a name="download-the-report-viewer-web-part-solution-package"></a>Descargar el paquete de solución del elemento web Visor de informes

El elemento web Visor de informes está disponible en el Centro de descarga de Microsoft.

[Descargar el paquete de solución del elemento web Visor de informes](https://www.microsoft.com/download/details.aspx?id=55949)

## <a name="considerations-and-limitations"></a>Consideraciones y limitaciones

Los elementos enumerados son específicos del elemento web Visor de informes actualizado.

* El elemento web solo puede usarse en páginas de SharePoint *clásico*.
* Solo se pueden insertar informes paginados (RDL) en el elemento web Visor de informes. Si quiere insertar informes de Power BI o informes móviles, puede usar el parámetro URL *rs:Embed=true*.

## <a name="next-steps"></a>Pasos siguientes

Para empezar a trabajar con el elemento web Visor de informes actualizado, vea [Implementar el elemento web Visor de informes en un sitio de SharePoint](deploy-report-viewer-web-part.md).
