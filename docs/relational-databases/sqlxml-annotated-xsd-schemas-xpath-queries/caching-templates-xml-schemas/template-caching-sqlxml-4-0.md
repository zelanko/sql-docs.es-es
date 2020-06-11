---
title: Almacenamiento en caché de plantillas (SQLXML)
description: Obtenga información acerca de cómo mejorar significativamente el rendimiento al ejecutar plantillas mediante el almacenamiento en caché de plantillas en SQLXML 4,0.
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- registry keys [SQLXML]
- cache [SQLXML]
- templates [SQLXML], caching
ms.assetid: 73e151c6-b24e-4422-a116-51e0846bc6f5
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8055210f85a23d37bb670091bd19cd4ce5c01663
ms.sourcegitcommit: 9921501952147b9ce3e85a1712495d5b3eb13e5b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/29/2020
ms.locfileid: "84215809"
---
# <a name="template-caching-sqlxml-40"></a>Almacenamiento en caché de plantillas (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Al almacenar las plantillas en la memoria caché mejora considerablemente el rendimiento. Si se establece el almacenamiento en caché de la plantilla, ésta permanece en memoria en su primera ejecución. Esto mejora el rendimiento de la próxima ejecución de la plantilla.  
  
 Puede establecer el tamaño de caché de la plantilla agregando la siguiente clave en el Registro:  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXML4\TemplateCacheSize  
```  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteRegistry](../../../includes/ssnoteregistry-md.md)]  
  
 El tamaño de la plantilla se debería establecer en función de la memoria disponible y del número de plantillas que se esté utilizando. El valor predeterminado de **TemplateCacheSize** size es 31. Puede aumentar el tamaño de caché si el acceso a la plantilla parece lento o puede reducirlo si hay poca memoria.  
  
 Para mejorar el rendimiento, se recomienda establecer **TemplateCacheSize** en un valor mayor que el número de plantillas que se suelen usar. Si **templatecachesize** es menor que el número de plantillas que tiene, el rendimiento se degrada a medida que aumenta el número de plantillas. El valor de **TemplateCacheSize** se puede establecer en un máximo de 128.  
  
 Cada vez que se utiliza una plantilla almacenada en la memoria caché, se comprueba el tiempo de modificación del archivo de plantilla para ver si es necesario actualizarlo. Esto se debe a que la copia en disco es más reciente que la copia en la caché.  
  
> [!NOTE]  
>  Los parámetros de plantilla y las propiedades de comandos no se almacenan en la memoria caché.  
  
## <a name="see-also"></a>Consulte también  
 [Almacenamiento en caché de esquemas &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/schema-caching-sqlxml-4-0.md)   
 [Almacenamiento en caché XSL &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/xsl-caching-sqlxml-4-0.md)  
  
  
