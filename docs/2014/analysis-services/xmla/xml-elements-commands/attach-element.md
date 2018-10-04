---
title: Elemento Attach | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- Attach command
ms.assetid: a315d1f1-e220-4296-97cb-6d35606b9640
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: eda22adcd9760fbeb01e009b0a8d9692f7e5d333
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48105405"
---
# <a name="attach-element"></a>Elemento Attach
  Adjunta una base de datos de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] , que previamente se ha separado de la instancia del servidor actual o de otra instancia, a la instancia del servidor actual.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Command>  
   <Attach>  
      <Folder>...</Folder>  
            <ReadWriteMode>...</ReadWriteMode>  
            <Password>...</Password>  
   </Attach>  
</Command>  
  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Command](../xml-elements-properties/command-element-xmla.md)|  
|Elementos secundarios|[Carpeta](../xml-elements-properties/folder-element-xmla.md)<br /><br /> [ReadWriteMode](../xml-elements-properties/readwritemode-element.md)<br /><br /> [Contraseña](../xml-elements-properties/password-element-xmla.md)|  
  
## <a name="see-also"></a>Vea también  
 <xref:Microsoft.AnalysisServices.Database.Detach%2A>   
 [Elemento Detach](detach-element.md)   
 [Adjuntar y separar bases de datos de Analysis Services](../../multidimensional-models/attach-and-detach-analysis-services-databases.md)   
 [Mover una base de datos de Analysis Services](../../multidimensional-models/move-an-analysis-services-database.md)   
 [ReadWriteModes de base de datos](../../multidimensional-models/database-readwritemodes.md)   
 [Cambiar una base de datos de Analysis Services entre los modos ReadOnly y ReadWrite](../../multidimensional-models/switch-an-analysis-services-database-between-readonly-and-readwrite-modes.md)  
  
  
