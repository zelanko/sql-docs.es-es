---
title: Elemento web Visor de en un sitio de SharePoint de informes | Documentos de Microsoft
ms.custom: 
ms.date: 09/25/2017
ms.prod: sql-server-2016
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
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: a37ed5efe7c365c601deb95d9fe761d227e7021e
ms.contentlocale: es-es
ms.lasthandoff: 10/06/2017

---
# <a name="report-viewer-web-part-on-a-sharepoint-site"></a>Notificar el elemento web Visor de en un sitio de SharePoint

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

El elemento web Visor de informes es un elemento web personalizado. Puede usar el elemento web para ver, navegar, imprimir y exportar informes en un servidor de informes dentro de un sitio de SharePoint. El elemento web Visor de informes está asociado a los archivos de definición (.rdl) de informes que se procesan por un servidor de informes de Microsoft SQL Server Reporting Services. 

El elemento web de Visor de informes más reciente también puede informes paginado de servicio implementados en el servidor de informes de Power BI. El elemento web no funciona con los informes de Power BI.

## <a name="why-the-report-viewer-web-part-is-re-introduced"></a>¿Por qué se vuelven a introducir el elemento web Visor de informes

El elemento web Visor de informes estaba disponible como parte del complemento de Reporting Services para productos de SharePoint. El elemento web era específico de servidores de informes en modo integrado de SharePoint. El modo integrado de SharePoint está en desuso después de SQL Server 2016.

A partir de SQL Server 2017, hay solo un modo de instalación de Reporting Services: **modo nativo**. Puede incrustar todos los tipos de informes utilizando el Visor de páginas web parte el *rs: incrustar = true* parámetro de dirección URL. Incrustar informes en las páginas de SharePoint es un caso de integración solicitado por los clientes y el elemento web de Visor de informes actualizado permite este escenario para informes paginados.

Mientras que el elemento web Visor de páginas es suficiente para incrustar un informe paginado en una página de SharePoint, el elemento web de Visor de informes actualizado ofrece características adicionales.

* Mostrar u ocultar los botones de barra de herramientas específica
* Invalidar los valores de parámetro de informe
* Conectar elementos web de filtro con parámetros de informe

## <a name="download-the-report-viewer-web-part-solution-package"></a>Descargar el paquete de solución de elementos de web de Visor de informes

El elemento web Visor de informes está disponible en Microsoft Download Center.

[Descargar paquete de solución de elementos de web de Visor de informes](https://www.microsoft.com/download/details.aspx?id=55949)

## <a name="considerations-and-limitations"></a>Consideraciones y limitaciones

Los elementos que aparecen son específicos al elemento web Visor de informes actualizado.

* El elemento web solo puede usarse en *clásico* páginas de SharePoint.
* Solo los informes (RDL) paginados se admiten para incrustar en el elemento web Visor de informes. Si desea para incrustar informes de Power BI o informes móviles, puede usar el *rs: incrustar = true* parámetro de dirección URL.

## <a name="next-steps"></a>Pasos siguientes

Para empezar a trabajar con el elemento web del Visor de informes actualizado, vea [implementar el elemento web Visor de informes en un sitio de SharePoint](deploy-report-viewer-web-part.md).
