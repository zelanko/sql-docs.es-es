---
title: Almacenamiento en caché XSL (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- registry keys [SQLXML]
- cache [SQLXML]
- XSL caching [SQLXML]
ms.assetid: 91994142-32f0-4d8d-a8cf-eb0d8b1f1999
caps.latest.revision: 21
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 64256db5e8cb147c47e28852bb3589e8732bf9c2
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37256017"
---
# <a name="xsl-caching-sqlxml-40"></a>Almacenamiento en caché XSL (SQLXML 4.0)
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
 [Almacenamiento en caché de plantilla &#40;SQLXML 4.0&#41;](template-caching-sqlxml-4-0.md)   
 [Almacenamiento en caché de esquema &#40;SQLXML 4.0&#41;](schema-caching-sqlxml-4-0.md)  
  
  
