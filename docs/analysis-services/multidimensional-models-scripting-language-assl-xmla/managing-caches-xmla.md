---
title: "Administración de cachés (XMLA) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- XMLA, cache
- XML for Analysis, cache
- clearing cache
- cache [Analysis Services]
ms.assetid: afad5c39-d4c3-4307-b3b9-a06617da0028
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 6dad9f3bb8c577ea8fb975d4f8ba4eac054f0a3e
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="managing-caches-xmla"></a>Administrar cachés (XMLA)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Puede usar el [ClearCache](../../analysis-services/xmla/xml-elements-commands/clearcache-element-xmla.md) comando XML for Analysis (XMLA) para borrar la memoria caché de una dimensión o partición especificada. Borrar la memoria caché se fuerza [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para volver a generar la memoria caché para ese objeto.  
  
## <a name="specifying-objects"></a>Especificar objetos  
 El [objeto](../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md) propiedad de la **ClearCache** comando puede contener una referencia de objeto sólo para uno de los siguientes objetos. Si se utiliza una referencia de objeto para un objeto distinto de los siguientes, se produce un error:  
  
 Base de datos  
 Borra la memoria caché para todas las dimensiones y particiones contenidas en la base de datos.  
  
 Dimensión  
 Borra la memoria caché para la dimensión especificada.  
  
 Cube  
 Borra la memoria caché para todas las particiones contenidas en los grupos de medida para el cubo.  
  
 Grupo de medida  
 Borra la memoria caché para todas las particiones contenidas en el grupo de medida.  
  
 Partición  
 Borra la memoria caché para la partición especificada.  
  
## <a name="see-also"></a>Vea también  
 [Desarrollo con XMLA en Analysis Services](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
