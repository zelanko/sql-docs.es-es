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
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 84f0b668407c89e1d6acc3c8cfbda73f129ca19a
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2020
ms.locfileid: "85439862"
---
# <a name="what39s-new-integration-services"></a>Qué&#39;s nuevo (Integration Services)
  [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)][!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]no ha cambiado con respecto a la versión anterior.  
  
 Para obtener información sobre otros [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] productos y tecnologías, consulte [novedades de SQL Server 2014](../sql-server/what-s-new-in-sql-server-2016.md).  
  
 Para obtener más información sobre los cambios relacionados con [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Business Intelligence, consulte [novedades de Analysis Services e inteligencia empresarial](https://docs.microsoft.com/analysis-services/what-s-new-in-analysis-services).  
  
##  <a name="rich-xml-validation-output-in-the-xml-task"></a><a name="ValidateXML"></a> Salida enriquecida de validación de XML en la tarea XML  
 Valide documentos XML y obtenga una salida de error enriquecida habilitando la propiedad `ValidationDetails` de la tarea XML. Antes de que la propiedad `ValidationDetails` estuviera disponible, la validación de XML efectuada mediante la tarea XML solo devolvía un resultado true o false, sin información sobre errores o sus ubicaciones. Ahora, cuando se establece `ValidationDetails` en true, el archivo de salida contiene información detallada sobre cada uno de los errores, incluido el número de línea y la posición. Puede usar esta información para comprender, buscar y corregir errores en documentos XML. Para obtener más información, vea [Validate XML with the XML Task](control-flow/xml-task.md).  
  
 [!INCLUDE[ssIS](../includes/ssis-md.md)] introdujo la propiedad `ValidationDetails` en [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] Service Pack 2. Esta nueva propiedad no se anunció ni documentó en su momento. La propiedad `ValidationDetails` también se encuentra disponible en [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] y en SQL Server 2016.  
  
## <a name="see-also"></a>Consulte también  
 [Características admitidas por las ediciones de SQL Server 2014](../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)  
  
  
