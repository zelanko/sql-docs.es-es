---
title: ¿Qué&#39;s nuevo (Integration Services)? | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services, what's new
- what's new [Integration Services]
ms.assetid: da6999c7-e5e3-4a59-a284-1da635995af1
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 5562b7424e4a104204becaed10378ffc999c4e98
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68891102"
---
# <a name="what39s-new-integration-services"></a>Qué&#39;s nuevo (Integration Services)
  [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)][!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] no ha cambiado con respecto a la versión anterior.  
  
 Para obtener información sobre [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] otros productos y tecnologías, consulte [novedades de SQL Server 2014](../sql-server/what-s-new-in-sql-server-2016.md).  
  
 Para obtener más información sobre los cambios [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] relacionados con Business Intelligence, consulte [novedades de Analysis Services e inteligencia empresarial](https://docs.microsoft.com/analysis-services/what-s-new-in-analysis-services).  
  
##  <a name="ValidateXML"></a>Resultado de la validación de XML enriquecida en la tarea XML  
 Valide documentos XML y obtenga una salida de error enriquecida habilitando la propiedad `ValidationDetails` de la tarea XML. Antes de que la propiedad `ValidationDetails` estuviera disponible, la validación de XML efectuada mediante la tarea XML solo devolvía un resultado true o false, sin información sobre errores o sus ubicaciones. Ahora, cuando se establece `ValidationDetails` en true, el archivo de salida contiene información detallada sobre cada uno de los errores, incluido el número de línea y la posición. Puede usar esta información para comprender, buscar y corregir errores en documentos XML. Para obtener más información, vea [Validate XML with the XML Task](control-flow/xml-task.md).  
  
 
  [!INCLUDE[ssIS](../includes/ssis-md.md)] introdujo la propiedad `ValidationDetails` en [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] Service Pack 2. Esta nueva propiedad no se anunció ni documentó en su momento. La propiedad `ValidationDetails` también se encuentra disponible en [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] y en SQL Server 2016.  
  
## <a name="see-also"></a>Consulte también  
 [Características compatibles con las ediciones de SQL Server 2014](../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)  
  
  
