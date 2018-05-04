---
title: Tipo de datos OlapDataSource (ASSL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/03/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- OlapDataSource Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- OlapDataSource
helpviewer_keywords:
- OlapDataSource data type
ms.assetid: cfe8937c-5f73-4773-a1e8-5e3310691966
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 0b19b0a1dc908671e55629310009d96607c6b685
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="olapdatasource-data-type-assl"></a>Tipo de datos OlapDataSource (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Define un tipo de datos derivado que representa un elemento [DataSource](../../../analysis-services/scripting/objects/datasource-element-assl.md) multidimensional.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<OlapDataSource>  
   <!-- Child elements are only those inherited from DataSource -->  
</OlapDataSource>  
```  
  
## <a name="data-type-characteristics"></a>Características del tipo de datos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipos de datos base|[Origen de datos](../../../analysis-services/scripting/data-type/datasource-data-type-assl.md)|  
|Tipos de datos derivados|Ninguno|  
  
## <a name="data-type-relationships"></a>Relaciones entre tipos de datos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|Ninguno|  
|Elementos secundarios|Ninguno|  
|Elementos derivados|[Origen de datos](../../../analysis-services/scripting/objects/datasource-element-assl.md) ([orígenes de datos](../../../analysis-services/scripting/collections/datasources-element-assl.md) colección de [base de datos](../../../analysis-services/scripting/objects/database-element-assl.md))|  
  
## <a name="remarks"></a>Comentarios  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.OlapDataSource>.  
  
## <a name="see-also"></a>Vea también  
 [Analysis Services Scripting Language tipos de datos XML & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
