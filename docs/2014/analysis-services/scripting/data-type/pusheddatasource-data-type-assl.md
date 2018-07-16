---
title: Tipo de datos PushedDataSource (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- PushedDataSource Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- PushedDataSource
helpviewer_keywords:
- PushedDataSource data type
ms.assetid: b319ee87-7c0a-41ec-a8af-cc7089aeb6ad
caps.latest.revision: 36
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 98309a1fa1706efaed47ab27cdf88d0b3e313fa5
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37235575"
---
# <a name="pusheddatasource-data-type-assl"></a>Tipo de datos PushedDataSource (ASSL)
  Define un tipo de datos primitivo que representa un origen de datos (como un [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] paquete) utilizado para "Insertar" datos en un [cubo](../objects/cube-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<PushedDataSource>  
   <Root>...</Root>  
   <EndOfData>...</EndOfData>  
</PushedDataSource>  
```  
  
## <a name="data-type-characteristics"></a>Características del tipo de datos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipos de datos básicos|None|  
|Tipos de datos derivados|None|  
  
## <a name="data-type-relationships"></a>Relaciones entre tipos de datos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|None|  
|Elementos secundarios|[EndOfData](../objects/data-element-assl.md), [raíz](../properties/root-element-assl.md)|  
|Elementos derivados|None|  
  
## <a name="remarks"></a>Notas  
 `PushedDataSource` solamente se utiliza dentro de un comando de procesamiento como un origen de datos fuera de línea. Los orígenes de datos almacenados no son nunca de este tipo.  
  
## <a name="see-also"></a>Vea también  
 [Tipos de datos XML de lenguaje Scripting de Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
