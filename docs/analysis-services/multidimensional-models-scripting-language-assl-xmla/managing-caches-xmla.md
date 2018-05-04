---
title: Administración de cachés (XMLA) | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6a34388f9c9d23d50fbd0de8842b8fc34f6bb8e4
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
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
  
  
