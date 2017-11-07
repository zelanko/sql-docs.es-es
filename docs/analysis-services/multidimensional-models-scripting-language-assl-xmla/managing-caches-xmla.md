---
title: "Administración de cachés (XMLA) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- XMLA, cache
- XML for Analysis, cache
- clearing cache
- cache [Analysis Services]
ms.assetid: afad5c39-d4c3-4307-b3b9-a06617da0028
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 69fc72149887598efe1c84c35c88fa24c7cdadbc
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="managing-caches-xmla"></a>Administrar cachés (XMLA)
  Puede usar el [ClearCache](../../analysis-services/xmla/xml-elements-commands/clearcache-element-xmla.md) comando XML for Analysis (XMLA) para borrar la memoria caché de una dimensión o partición especificada. Borrar la memoria caché se fuerza [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para volver a generar la memoria caché para ese objeto.  
  
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
 [Desarrollar con XMLA en Analysis Services](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  

