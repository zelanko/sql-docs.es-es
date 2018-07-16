---
title: Elemento de grupo de archivos de índice (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Filegroup element [DTA]
ms.assetid: 7078d2fb-fa77-44fc-beb3-c095088fcb85
caps.latest.revision: 12
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: fad6406d6a719ebd33f48a4cd7c0cf7c2c0e7122
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37244115"
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
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|**Tipo y longitud de los datos**|`string`, longitud ilimitada.|  
|**Valor predeterminado**|Ninguno.|  
|**Repetición**|Opcional. Puede utilizar una vez por cada `Index` elemento. Este elemento no se puede usar si la `PartitionScheme` y `PartitionColumn` elementos se especifican para el `Index` elemento.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elementos|  
|------------------|--------------|  
|**Elemento primario**|[Elemento de índice &#40;DTA&#41;](index-element-dta.md)|  
|**Elementos secundarios**|Ninguno.|  
  
## <a name="example"></a>Ejemplo  
 Para obtener un ejemplo de uso de este elemento, vea [Ejemplo de archivo de entrada XML con configuración especificada por el usuario &#40;DTA&#41;](xml-input-file-sample-with-user-specified-configuration-dta.md).  
  
## <a name="see-also"></a>Vea también  
 [Referencia del archivo de entrada XML &#40;Asistente para la optimización de motor de base de datos&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
