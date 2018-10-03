---
title: Nombre de elemento de servidor (DTA) | Microsoft Docs
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
ms.assetid: 4c94754d-6d62-4357-8ce7-f107ebf90c71
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4c3c41cf90d15ee8c5342dd0274cd8fedbd30dee
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48171535"
---
# <a name="name-element-for-server-dta"></a>Name (DTA, elemento de Server)
  Contiene el nombre del servidor en el que residen las bases de datos que se desean optimizar.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
...code removed here...  
<Server>  
    <Name>...</Name>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|**Tipo y longitud de los datos**|`string`, entre 1 y 255 caracteres.|  
|**Valor predeterminado**|Ninguno.|  
|**Repetición**|Una obligatoria por elemento **Server** .|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elementos|  
|------------------|--------------|  
|**Elemento primario**|[Elemento Server &#40;DTA&#41;](server-element-dta.md)|  
|**Elementos secundarios**|Ninguno.|  
  
## <a name="example"></a>Ejemplo  
 Para obtener un ejemplo de cómo se usa el elemento **Name** , vea [Server Element &#40;DTA&#41;](server-element-dta.md).  
  
## <a name="see-also"></a>Vea también  
 [Referencia del archivo de entrada XML &#40;Asistente para la optimización de motor de base de datos&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
