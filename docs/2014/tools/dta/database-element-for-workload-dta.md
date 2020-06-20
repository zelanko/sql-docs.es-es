---
title: Database (DTA, elemento de Workload) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Database element
ms.assetid: 112fca2a-37e5-4162-b2e7-b56eb8ab0c6f
author: stevestein
ms.author: sstein
ms.openlocfilehash: 48f9202483bcb2cf8e06b6e0d14834753cc666b8
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85000394"
---
# <a name="database-element-for-workload-dta"></a>Database (DTA, elemento de Workload)
  Especifica la base de datos en la que se ubica la tabla de seguimiento de la carga de trabajo.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
<Workload>  
  <Database>  
   ...code removed here...  
  </Database>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|**Tipo y longitud de los datos**|Ninguno.|  
|**Valor predeterminado**|Ninguno.|  
|**Repetición**|Una obligatoria si no se especifica ningún otro tipo de carga de trabajo. Es necesario especificar un elemento secundario `EventString`, `File` o `Database` para el elemento primario `Workload`, aunque solo se puede utilizar un tipo. Por ejemplo, si se especifica una carga de trabajo con el `Database` elemento, no se puede especificar una carga de trabajo con el `File` elemento en el mismo archivo de entrada XML.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elementos|  
|------------------|--------------|  
|**Elemento primario**|[Workload &#40;DTA, elemento&#41;](workload-element-dta.md)|  
|**Elementos secundarios**|[Name &#40;DTA, elemento de Database&#41;](name-element-for-database-dta.md)<br /><br /> [Schema &#40;DTA, elemento de Database&#41;](schema-element-for-database-dta.md)|  
  
## <a name="remarks"></a>Observaciones  
 Este elemento tiene el nombre **DatabaseDetailsTypecomplexType** en el esquema XML del Asistente para la optimización de motor de base de datos. No confunda este elemento `Database` con el que tiene al elemento `Configuration` como raíz primaria. (Vea [Elemento Database de Configuration &#40;DTA&#41;](database-element-for-configuration-dta.md)).  
  
## <a name="example"></a>Ejemplo  
 Para obtener un ejemplo de uso de este `Database` elemento, vea el ejemplo de código del [elemento Workload &#40;DTA&#41;](workload-element-dta.md).  
  
## <a name="see-also"></a>Consulte también  
 [Referencia del archivo de entrada XML &#40;Asistente para la optimización de motor de base de datos&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
