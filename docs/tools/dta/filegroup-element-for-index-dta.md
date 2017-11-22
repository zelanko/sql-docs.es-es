---
title: Grupo de archivos, elemento de Index (DTA) | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: XML
helpviewer_keywords: Filegroup element [DTA]
ms.assetid: 7078d2fb-fa77-44fc-beb3-c095088fcb85
caps.latest.revision: "12"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: cfea77c2696e85fff1b79a1b1ce7725caafa7817
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="filegroup-element-for-index-dta"></a>Filegroup (DTA, elemento de Index)
  Especifica el grupo de archivos de una configuración especificada por el usuario en que se va a crear el índice.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
<Index>  
  <Name>...</Name>  
  <Column>  
    <Name>...</Name>  
  <Filegroup>...</Filegroup>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|**Tipo y longitud de los datos**|**string**, longitud ilimitada.|  
|**Valor predeterminado**|Ninguno.|  
|**Repetición**|Opcional. Se puede utilizar una vez por cada elemento **Index** . Este elemento no se puede utilizar si se han especificado los elementos **PartitionScheme** y **PartitionColumn** para el elemento **Index** .|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elementos|  
|------------------|--------------|  
|**Elemento primario**|[Index &#40;DTA, elemento&#41;](../../tools/dta/index-element-dta.md)|  
|**Elementos secundarios**|Ninguno.|  
  
## <a name="example"></a>Ejemplo  
 Para obtener un ejemplo de uso de este elemento, vea [Ejemplo de archivo de entrada XML con configuración especificada por el usuario &#40;DTA&#41;](../../tools/dta/xml-input-file-sample-with-user-specified-configuration-dta.md).  
  
## <a name="see-also"></a>Vea también  
 [Referencia del archivo de entrada XML &#40;Asistente para la optimización de motor de base de datos&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
