---
title: Elemento de la base de datos para la carga de trabajo (DTA) | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- XML
helpviewer_keywords:
- Database element
ms.assetid: 112fca2a-37e5-4162-b2e7-b56eb8ab0c6f
caps.latest.revision: 12
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e71d9a3077821fc4b34ee5cebac5441065ddf013
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

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
|**Repetición**|Una obligatoria si no se especifica ningún otro tipo de carga de trabajo. Es necesario especificar un elemento secundario **EventString**, **File**o **Database** para el elemento primario **Workload** , aunque solo se puede utilizar un tipo. Por ejemplo, si se especifica una carga de trabajo con el elemento **Database** , no se puede especificar una carga de trabajo con el elemento **File** en el mismo archivo de entrada XML.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elementos|  
|------------------|--------------|  
|**Elemento primario**|[Workload, elemento &#40; DTA &#41;](../../tools/dta/workload-element-dta.md)|  
|**Elementos secundarios**|[Elemento de nombre de base de datos &#40; DTA &#41;](../../tools/dta/name-element-for-database-dta.md)<br /><br /> [Elemento Schema de Database &#40;DTA&#41;](../../tools/dta/schema-element-for-database-dta.md)|  
  
## <a name="remarks"></a>Comentarios  
 Este elemento tiene el nombre **DatabaseDetailsTypecomplexType** en el esquema XML del Asistente para la optimización de motor de base de datos. No confunda este elemento **Database** con el que tiene al elemento **Configuration** como raíz primaria. (Vea [Elemento Database de Configuration &#40;DTA&#41;](../../tools/dta/database-element-for-configuration-dta.md)).  
  
## <a name="example"></a>Ejemplo  
 Para obtener un ejemplo del uso de este elemento **Database** , vea el ejemplo de código en [Workload &#40;DTA, elemento&#41;](../../tools/dta/workload-element-dta.md).  
  
## <a name="see-also"></a>Vea también  
 [Referencia del archivo de entrada XML &#40;Asistente para la optimización de motor de base de datos&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  

