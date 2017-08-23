---
title: Origen OData | Documentos de Microsoft
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.DTS.DESIGNER.ODATASOURCE.F1
ms.assetid: cc9003c9-638e-432b-867e-e949d50cec90
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c52506dcfa582cc3e0992fe4fda772489d544247
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="odata-source"></a>Origen OData
  Use el componente de origen OData en un paquete SSIS para consumir datos de un servicio de Open Data Protocol (OData). El componente admite los protocolos OData v3 y v4.  
  
-   Para el protocolo OData V3, el componente admite los formatos de datos ATOM y JSON.  
  
-   Para el protocolo OData V4, el componente admite el formato de datos JSON.  
  
> [!NOTE]  
>  También puede usar el origen OData para leer listas de SharePoint. Para ver todas las listas en un servidor de SharePoint, use la siguiente dirección URL: http://\<server > / _vti_bin/ListData.svc. Para obtener más información sobre las convenciones de direcciones URL de SharePoint, vea [Interfaz de REST de SharePoint Foundation](http://msdn.microsoft.com/library/ff521587.aspx).  El origen OData ahora es compatible con productos de Microsoft Dynamics AX Online y Microsoft Dynamics CRM Online.
  
## <a name="odata-format"></a>Formato OData  
 La mayoría de los servicios OData devuelven resultados en varios formatos. Puede especificar el formato del conjunto de resultados mediante la opción de consulta $format. Los formatos como JSON y JSON Light son más eficaces que ATOM o XML, y pueden conseguir mejor rendimiento cuando se transfieren grandes cantidades de datos. En la tabla siguiente se muestran resultados de pruebas de ejemplo. Como puede ver, hubo una mejora del rendimiento del 30-53 % al cambiar de ATOM a JSON y del 67 % cuando se cambió de ATOM al nuevo formato JSON Light (disponible en WCF Data Services 5.1).  
  
|||||  
|-|-|-|-|  
|Filas|ATOM|JSON|JSON (Light)|  
|10000|113 segundos|74 segundos|68 segundos|  
|1000000|1110 segundos|853 segundos|665 segundos|  
  
> [!NOTE]  
>  El origen OData de SSIS usa 5.6.1 para analizar las fuentes de OData V3 y ODataLib 6.12.0 para analizar las fuentes de OData V4.  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Tutorial: Usar el origen OData](../../integration-services/data-flow/tutorial-using-the-odata-source.md)  
  
-   [Modificar una consulta de origen OData en tiempo de ejecución](../../integration-services/data-flow/modify-odata-source-query-at-runtime.md)  
  
-   [Editor de origen OData &#40;página Conexión&#41;](../../integration-services/data-flow/odata-source-editor-connection-page.md)  
  
-   [Editor de origen OData &#40;página Columnas&#41;](../../integration-services/data-flow/odata-source-editor-columns-page.md)  
  
-   [Editor de origen OData &#40;página Salida de error&#41;](../../integration-services/data-flow/odata-source-editor-error-output-page.md)  
  
-   [Propiedades del origen OData](../../integration-services/data-flow/odata-source-properties.md)  
  
## <a name="see-also"></a>Vea también  
 [Administrador de conexiones OData](../../integration-services/connection-manager/odata-connection-manager.md)  
  
  
