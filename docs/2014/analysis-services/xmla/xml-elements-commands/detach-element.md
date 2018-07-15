---
title: Elemento Detach | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- Detach command
ms.assetid: adbc7920-2a4a-4842-9e6f-37006fa19ff8
caps.latest.revision: 10
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4da654dd7b6af196f8ca2ac9c3efeb6e0b23ed45
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37217955"
---
# <a name="detach-element"></a>Elemento Detach
  Separa una base de datos de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] de la instancia del servidor actual.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Command>  
   <Detach>  
      <Object>...</Object>  
      <Password>...</Password>  
   </Detach>  
</Command>  
  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Command](../xml-elements-properties/command-element-xmla.md)|  
|Elementos secundarios|[Objeto](../xml-elements-properties/object-element-xmla.md)<br /><br /> [Contraseña](../xml-elements-properties/password-element-xmla.md)|  
  
## <a name="see-also"></a>Vea también  
 <xref:Microsoft.AnalysisServices.Database.Detach%2A>   
 [Elemento Attach](attach-element.md)   
 [Adjuntar y separar bases de datos de Analysis Services](../../multidimensional-models/attach-and-detach-analysis-services-databases.md)   
 [Mover una base de datos de Analysis Services](../../multidimensional-models/move-an-analysis-services-database.md)   
 [ReadWriteModes de base de datos](../../multidimensional-models/database-readwritemodes.md)   
 [Cambiar una base de datos de Analysis Services entre los modos ReadOnly y ReadWrite](../../multidimensional-models/switch-an-analysis-services-database-between-readonly-and-readwrite-modes.md)  
  
  
