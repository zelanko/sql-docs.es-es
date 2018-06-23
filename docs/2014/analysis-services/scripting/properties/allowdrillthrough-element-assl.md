---
title: Elemento AllowDrillThrough (ASSL) | Documentos de Microsoft
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
api_name:
- AllowDrillThrough Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AllowDrillThrough
helpviewer_keywords:
- AllowDrillThrough element
ms.assetid: 53c9e4a3-a376-447d-a13f-80d845cc9789
caps.latest.revision: 51
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: e5ee132903b98c616ce756b423455302ca6e65f4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36111888"
---
# <a name="allowdrillthrough-element-assl"></a>Elemento AllowDrillThrough (ASSL)
  Determina si se permite la obtención de detalles para el elemento primario.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<MiningModel> <!-- or MiningModelPermission -->  
<!-- or MiningStructurePermission -->   ...  
   <AllowDrillThrough>...</AllowDrillThrough>  
   ...  
</MiningModel>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Boolean|  
|Valor predeterminado|`False`|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Elemento MiningModel](../objects/miningmodel-element-assl.md), [MiningModelPermission](../objects/miningmodelpermission-element-assl.md), [MiningStructurePermission](../objects/miningstructurepermission-element-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 Los elementos que corresponden a los elementos primarios de `AllowDrillThrough` en el modelo de objetos de Objetos de administración de análisis (AMO) son <xref:Microsoft.AnalysisServices.MiningModel>, <xref:Microsoft.AnalysisServices.MiningModelPermission> y <xref:Microsoft.AnalysisServices.MiningStructurePermission>.  
  
## <a name="drillthrough-on-mining-structures"></a>Obtención de detalles en estructuras de minería de datos  
 En [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], puede definir `AllowDrillthrough` permisos para estructuras de minería de datos, así como los modelos de minería de datos. Cuando se asigna este permiso a un rol, cualquier miembro de ese rol puede consultar el modelo de minería de datos y devolver columnas de estructura que no estaban incluidas en el modelo. Por ejemplo, se puede crear un modelo que utiliza solamente estas columnas: clave de clientes, ingresos de clientes y compras de clientes. Si habilita la obtención de detalles en el modelo, los usuarios pueden devolver información en otras columnas de la estructura de minería de datos, como nombres o correos electrónicos de clientes.  
  
 Por consiguiente, para proteger los datos confidenciales, se debe tener precaución al agregar columnas a la estructura de minería de datos. Además, solo se debe conceder el permiso `AllowDrillthrough` en una estructura cuando sea necesario.  
  
 Para obtener detalles en columnas de estructura, utilice una consulta con uno de los formatos siguientes:  
  
 `SELECT * FROM <structure>.CASES`  
  
 o Administrador de configuración de  
  
 `SELECT StructureColumn('<structure-column-name>') FROM <model>.CASES`  
  
## <a name="see-also"></a>Vea también  
 [Elemento role &#40;ASSL&#41;](../objects/role-element-assl.md)   
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  