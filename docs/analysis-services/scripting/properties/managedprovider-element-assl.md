---
title: Elemento ManagedProvider (ASSL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- ManagedProvider Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- ManagedProvider element
ms.assetid: ed5a1077-20a4-40b9-b62d-0db0d53b9624
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a29aaf1e342774f1e436e4d63b0b3ecdebd493cc
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="managedprovider-element-assl"></a>Elemento ManagedProvider (ASSL)
  Contiene el nombre del proveedor administrado utilizado por un elemento derivado de la [DataSource](../../../analysis-services/scripting/data-type/datasource-data-type-assl.md) tipo de datos.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<DataSource>  
   ...  
   <ManagedProvider>...</ManagedProvider>  
   ...  
</DataSource>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Cadena|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[Origen de datos](../../../analysis-services/scripting/data-type/datasource-data-type-assl.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 Si un origen de datos utiliza un proveedor administrado, el elemento **ManagedProvider** contiene el nombre del proveedor administrado.  
  
## <a name="see-also"></a>Vea también  
 [Name, elemento &#40; ASSL &#41;](../../../analysis-services/scripting/properties/name-element-assl.md)   
 [Propiedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

