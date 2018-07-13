---
title: Administración de cachés (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- XMLA, cache
- XML for Analysis, cache
- clearing cache
- cache [Analysis Services]
ms.assetid: afad5c39-d4c3-4307-b3b9-a06617da0028
caps.latest.revision: 13
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: da13c86e86a2f51719a9d4f0aedfda33935766ae
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37180822"
---
# <a name="managing-caches-xmla"></a>Administrar cachés (XMLA)
  Puede usar el [ClearCache](../xmla/xml-elements-commands/clearcache-element-xmla.md) comando XML for Analysis (XMLA) para borrar la caché de una dimensión o partición especificada. Borrar la memoria caché las fuerzas [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para recompilar la memoria caché para ese objeto.  
  
## <a name="specifying-objects"></a>Especificar objetos  
 El [objeto](../xmla/xml-elements-properties/object-element-xmla.md) propiedad de la `ClearCache` comando puede contener una referencia de objeto únicamente para uno de los siguientes objetos. Si se utiliza una referencia de objeto para un objeto distinto de los siguientes, se produce un error:  
  
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
 [Desarrollo con XMLA en Analysis Services](developing-with-xmla-in-analysis-services.md)  
  
  
