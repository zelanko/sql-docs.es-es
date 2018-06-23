---
title: Elemento de la base de datos para la carga de trabajo (DTA) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- XML
helpviewer_keywords:
- Database element
ms.assetid: 112fca2a-37e5-4162-b2e7-b56eb8ab0c6f
caps.latest.revision: 12
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 6380708319286a984ef54ef3820fab22821047bf
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36107520"
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
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|**Tipo y longitud de los datos**|Ninguno.|  
|**Valor predeterminado**|Ninguno.|  
|**Repetición**|Una obligatoria si no se especifica ningún otro tipo de carga de trabajo. Debe especificar un `EventString`, `File`, o un `Database` elemento secundario para el `Workload` primario, pero solo un tipo puede utilizarse. Por ejemplo, si especifica una carga de trabajo con el `Database` elemento, no se puede especificar también una carga de trabajo con el `File` elemento en el mismo archivo de entrada XML.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elementos|  
|------------------|--------------|  
|**Elemento primario**|[Workload, elemento &#40;DTA&#41;](workload-element-dta.md)|  
|**Elementos secundarios**|[El nombre de elemento de base de datos &#40;DTA&#41;](name-element-for-database-dta.md)<br /><br /> [Elemento de esquema de base de datos &#40;DTA&#41;](schema-element-for-database-dta.md)|  
  
## <a name="remarks"></a>Notas  
 Este elemento tiene el nombre **DatabaseDetailsTypecomplexType** en el esquema XML del Asistente para la optimización de motor de base de datos. No confunda este elemento `Database` con el que tiene al elemento `Configuration` como raíz primaria. (Vea [Elemento Database de Configuration &#40;DTA&#41;](database-element-for-configuration-dta.md)).  
  
## <a name="example"></a>Ejemplo  
 Para obtener un ejemplo de uso de este `Database` elemento, vea el ejemplo de código de [Workload, elemento &#40;DTA&#41;](workload-element-dta.md).  
  
## <a name="see-also"></a>Vea también  
 [Referencia del archivo de entrada XML &#40;Asistente para la optimización de motor de base de datos&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  