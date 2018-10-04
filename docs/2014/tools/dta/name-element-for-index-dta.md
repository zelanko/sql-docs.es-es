---
title: Nombre de elemento para el índice (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Name element
ms.assetid: 2300e9cf-f0a8-49e6-b1f5-45ffe03ccb5f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c22ac7cd34a6cc762da47ec00fd42d183dbac045
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48116258"
---
# <a name="name-element-for-index-dta"></a>Name (DTA, elemento de Index)
  Establece un nombre para un índice en la configuración especificada por el usuario.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
<Create>  
    <Index>  
        <Name>...</Name>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|**Tipo y longitud de los datos**|`string`, longitud ilimitada.|  
|**Valor predeterminado**|Ninguno.|  
|**Repetición**|Una obligatoria por cada `Index` elemento.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elementos|  
|------------------|--------------|  
|**Elemento primario**|[Elemento de índice &#40;DTA&#41;](index-element-dta.md)|  
|**Elementos secundarios**|Ninguno.|  
  
## <a name="example"></a>Ejemplo  
 Para obtener un ejemplo de uso de este elemento, vea [Ejemplo de archivo de entrada XML con configuración especificada por el usuario &#40;DTA&#41;](xml-input-file-sample-with-user-specified-configuration-dta.md).  
  
## <a name="see-also"></a>Vea también  
 [Referencia del archivo de entrada XML &#40;Asistente para la optimización de motor de base de datos&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
