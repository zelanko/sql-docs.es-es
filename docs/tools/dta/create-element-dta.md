---
title: "Create (DTA, elemento) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "XML"
helpviewer_keywords: 
  - "Create (DTA, elemento)"
ms.assetid: 9d076c90-f933-45f4-b6d9-447793f6528b
caps.latest.revision: 12
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 12
---
# Create (DTA, elemento)
  Contiene información sobre los índices, las estadísticas o las estructuras de montones de una configuración especificada por el usuario.  
  
## Sintaxis  
  
```  
  
<Recommendation>  
    <Create>  
    ...code removed here...  
    </Create>  
</Recommendation>  
```  
  
## Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|**Tipo y longitud de los datos**|Ninguno.|  
|**Valor predeterminado**|Ninguno.|  
|**Repetición**|Una obligatoria por cada tipo de estructura de diseño físico (índices, estadísticas o estructuras de montones).|  
  
## Relaciones del elemento  
  
|Relación|Elementos|  
|------------------|--------------|  
|**Elemento primario**|[Elemento Recommendation &#40;DTA&#41;](../../tools/dta/recommendation-element-dta.md)|  
|**Elementos secundarios**|[Index &#40;DTA, elemento&#41;](../../tools/dta/index-element-dta.md)<br /><br /> Elemento **Statistics** (para obtener más información, vea el [esquema XML del Asistente para la optimización de motor de base de datos](http://schemas.microsoft.com/sqlserver/)).<br /><br /> Elemento **Heap** (para obtener más información, vea el [esquema XML del Asistente para la optimización de motor de base de datos](http://schemas.microsoft.com/sqlserver/)).|  
  
## Comentarios  
 Este elemento tiene el nombre **CreateTypecomplexType** en el esquema XML del Asistente para la optimización de motor de base de datos. Se utiliza para crear los índices, las estadísticas y las estructuras de montones de una configuración especificada por el usuario. No confunda este elemento **Create** con los otros tipos que se pueden usar para crear vistas (**CreateViewType**) o particiones (**CreatePType**). Vea el [esquema XML del Asistente para la optimización de motor de base de datos](http://schemas.microsoft.com/sqlserver/) para obtener más información sobre estos otros tipos de elementos **Create**.  
  
## Ejemplo  
 Para obtener un ejemplo de uso de este elemento, vea [Ejemplo de archivo de entrada XML con configuración especificada por el usuario &#40;DTA&#41;](../../tools/dta/xml-input-file-sample-with-user-specified-configuration-dta.md).  
  
## Vea también  
 [Referencia del archivo de entrada XML &#40;Asistente para la optimización de motor de base de datos&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  