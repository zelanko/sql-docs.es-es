---
title: ¿Qué&#39;s nuevo (Integration Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services, what's new
- what's new [Integration Services]
ms.assetid: da6999c7-e5e3-4a59-a284-1da635995af1
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7427402df49625c04ab7d1c38dd6bcfe3298e0ed
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48048545"
---
# <a name="what39s-new-integration-services"></a>¿Qué&#39;s nuevo (Integration Services)
  [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] no ha cambiado respecto a la versión anterior.  
  
 Para obtener información acerca de otros [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] productos y tecnologías, consulte [What ' s New in SQL Server 2014](../sql-server/what-s-new-in-sql-server-2016.md).  
  
 Para obtener más información acerca de los cambios relacionados con [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Business Intelligence, consulte [What ' s New in Analysis Services y Business Intelligence](../analysis-services/what-s-new-in-analysis-services.md).  
  
##  <a name="ValidateXML"></a> Salida enriquecida de validación de XML en la tarea XML  
 Validar documentos XML y obtenga la salida de error enriquecida habilitando la `ValidationDetails` propiedad de la tarea XML. Antes de la `ValidationDetails` propiedad estaba disponible, validación de XML mediante la tarea XML devuelve solo un resultado true o false, sin información sobre errores o sus ubicaciones. Ahora, al establecer `ValidationDetails` en true, la salida de archivo contiene información detallada sobre cada error, incluido el número de línea y la posición. Puede usar esta información para comprender, buscar y corregir errores en documentos XML. Para obtener más información, vea [Validate XML with the XML Task](control-flow/xml-task.md).  
  
 [!INCLUDE[ssIS](../includes/ssis-md.md)] introdujo el `ValidationDetails` propiedad [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] Service Pack 2. Esta nueva propiedad no se anunció ni documentó en su momento. El `ValidationDetails` también está disponible en la propiedad [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] y en SQL Server 2016.  
  
## <a name="see-also"></a>Vea también  
 [Características compatibles con las ediciones de SQL Server 2014](../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)  
  
  
