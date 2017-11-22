---
title: "Plantilla de almacenamiento en caché (SQLXML 4.0) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: sqlxml
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- registry keys [SQLXML]
- cache [SQLXML]
- templates [SQLXML], caching
ms.assetid: 73e151c6-b24e-4422-a116-51e0846bc6f5
caps.latest.revision: "25"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0be646f13db19d52a71b248bf3a97f3ae60f5051
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="template-caching-sqlxml-40"></a>Almacenamiento en caché de plantillas (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]Almacenamiento en caché de plantilla mejora notablemente el rendimiento. Si se establece el almacenamiento en caché de la plantilla, ésta permanece en memoria en su primera ejecución. Esto mejora el rendimiento de la próxima ejecución de la plantilla.  
  
 Puede establecer el tamaño de caché de la plantilla agregando la siguiente clave en el Registro:  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXML4\TemplateCacheSize  
```  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteRegistry](../../../includes/ssnoteregistry-md.md)]  
  
 El tamaño de la plantilla se debería establecer en función de la memoria disponible y del número de plantillas que se esté utilizando. El valor predeterminado de **TemplateCacheSize** es 31. Puede aumentar el tamaño de caché si el acceso a la plantilla parece lento o puede reducirlo si hay poca memoria.  
  
 Para mejorar el rendimiento, se recomienda que establezca **TemplateCacheSize** mayor que el número de plantillas que normalmente utiliza. Si **Templatecachesize** es menor que el número de plantillas que tiene, el rendimiento se degrada como el número de aumento de plantillas. El **TemplateCacheSize** se puede establecer en un máximo de 128.  
  
 Cada vez que se utiliza una plantilla almacenada en la memoria caché, se comprueba el tiempo de modificación del archivo de plantilla para ver si es necesario actualizarlo. Esto se debe a que la copia en disco es más reciente que la copia en la caché.  
  
> [!NOTE]  
>  Los parámetros de plantilla y las propiedades de comandos no se almacenan en la memoria caché.  
  
## <a name="see-also"></a>Vea también  
 [Almacenamiento en caché de esquema &#40; SQLXML 4.0 &#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/schema-caching-sqlxml-4-0.md)   
 [Almacenamiento en caché XSL &#40; SQLXML 4.0 &#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/xsl-caching-sqlxml-4-0.md)  
  
  
