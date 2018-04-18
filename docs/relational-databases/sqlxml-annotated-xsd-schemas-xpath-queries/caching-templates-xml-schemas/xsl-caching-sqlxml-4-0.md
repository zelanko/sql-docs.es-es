---
title: Almacenamiento en caché XSL (SQLXML 4.0) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- registry keys [SQLXML]
- cache [SQLXML]
- XSL caching [SQLXML]
ms.assetid: 91994142-32f0-4d8d-a8cf-eb0d8b1f1999
caps.latest.revision: 24
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: c14703a0156c420d072b28d726400a1331d06477
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="xsl-caching-sqlxml-40"></a>Almacenamiento en caché XSL (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Cuando se almacenan en caché hojas de estilos XSL, se mejora rendimiento. En su primera ejecución, una hoja de estilos XSL permanece en memoria si el almacenamiento en caché XSL está establecido en ON; esto mejora el rendimiento en el procesamiento posterior. El valor predeterminado es ON.  
  
 Puede establecer el tamaño de la caché de XSL agregando la siguiente clave en el Registro:  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXML4\XSLCacheSize  
```  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteRegistry](../../../includes/ssnoteregistry-md.md)]  
  
 El tamaño de la caché de XSL se debería establecer en base a la memoria disponible y el número de hojas de estilos XSL que está utilizando. El valor predeterminado de **XSLCacheSize** es 31. Puede aumentar el tamaño de la caché si el acceso a XSL parece lento o puede reducirlo si hay poca memoria.  
  
 Para mejorar el rendimiento, es recomendable que establezca **XSLCacheSize** en un valor más alto que el número de hojas de estilos XSL que normalmente utiliza. Si **XSLCacheSize** es menor que el número que tiene de hojas de estilos XSL, el rendimiento es peor a medida que el número de hojas de estilos de XSL aumenta. **XSLCacheSize** puede estar establecido en un máximo de 128.  
  
 Cada vez que se usa la hoja de estilos XSL almacenada en caché, se comprueba el tiempo de modificación del archivo XSL para determinar si se debe actualizar. Esto se debe a que la copia en disco es más reciente que la copia en la caché.  
  
## <a name="see-also"></a>Vea también  
 [Almacenamiento en caché de plantilla & #40; SQLXML 4.0 & #41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/template-caching-sqlxml-4-0.md)   
 [Almacenamiento en caché de esquema & #40; SQLXML 4.0 & #41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/schema-caching-sqlxml-4-0.md)  
  
  
