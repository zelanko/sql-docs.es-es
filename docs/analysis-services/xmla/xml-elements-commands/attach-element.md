---
title: Elemento Attach | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: fa13ada270ffe7c7d7a1290dd3645efae5f4c6a1
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "38015728"
---
# <a name="attach-element"></a>Elemento Attach
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Adjunta una base de datos de Analysis Services que previamente se ha separado de la instancia de servidor actual o desde otra instancia, a la instancia de servidor actual.  
  
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
  
## <a name="element-relationships"></a>Relaciones de elementos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Command](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|Elementos secundarios|[Carpeta](../../../analysis-services/xmla/xml-elements-properties/folder-element-xmla.md)<br /><br /> [ReadWriteMode](../../../analysis-services/xmla/xml-elements-properties/readwritemode-element.md)<br /><br /> [Contraseña](../../../analysis-services/xmla/xml-elements-properties/password-element-xmla.md)|  
  
## <a name="see-also"></a>Vea también
 <xref:Microsoft.AnalysisServices.Database.Detach%2A>   
 [Elemento Detach](../../../analysis-services/xmla/xml-elements-commands/detach-element.md)   
 [Adjuntar y separar bases de datos de Analysis Services](../../../analysis-services/multidimensional-models/attach-and-detach-analysis-services-databases.md)   
 [Mover una base de datos de Analysis Services](../../../analysis-services/multidimensional-models/move-an-analysis-services-database.md)   
 [ReadWriteModes de base de datos](../../../analysis-services/multidimensional-models/database-readwritemodes.md)   
 [Cambiar una base de datos de Analysis Services entre los modos ReadOnly y ReadWrite](../../../analysis-services/multidimensional-models/switch-an-analysis-services-database-between-readonly-and-readwrite-modes.md)  
  
  
