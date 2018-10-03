---
title: Elemento Administer (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Administer Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Administer
helpviewer_keywords:
- Administer element
ms.assetid: 52924cd6-6176-47c8-ab17-4ee0e0ce42b1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 682c65420383bcd3db70d1c477781c7db1193334
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48149305"
---
# <a name="administer-element-assl"></a>Elemento Administer (ASSL)
  Indica si el permiso asociado incluye el derecho a administrar un [base de datos](../objects/database-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<DatabasePermission>  
      ...  
      <Administer>...</Administer>  
   ...  
</DatabasePermission>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Boolean|  
|Valor predeterminado|False|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Elemento DatabasePermission](../objects/databasepermission-element-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Comentarios  
 El elemento `Administer` indica si un usuario puede realizar funciones administrativas solo en la base de datos especificada. El rol de administrador del servidor puede realizar funciones administrativas en todas las bases de datos que contiene la instancia.  
  
 El elemento que se corresponde con el elemento primario de `Administer` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.DatabasePermission>.  
  
## <a name="see-also"></a>Vea también  
 [Tipo de datos Permission &#40;ASSL&#41;](../data-type/permission-data-type-assl.md)   
 [Elemento role &#40;ASSL&#41;](../objects/role-element-assl.md)   
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  
