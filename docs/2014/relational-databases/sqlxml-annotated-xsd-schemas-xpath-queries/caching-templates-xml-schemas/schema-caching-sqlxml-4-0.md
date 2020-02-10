---
title: Almacenamiento en caché de esquemas (SQLXML 4,0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- registry keys [SQLXML]
- cache [SQLXML]
- schemas [SQLXML]
ms.assetid: 7e5fda21-b435-41fd-b637-8b616560a93f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6ca536125be481766e41c3665dd313d483160ae0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66013275"
---
# <a name="schema-caching-sqlxml-40"></a>Almacenamiento de esquemas en caché (SQLXML 4.0)
  Con una instalación simultánea de XML para Microsoft SQL Server 2000 Web Release 1, Microsoft SQLXML 2.0 y SQLXML 3.0, puede controlar de forma explícita el almacenamiento en caché de esquemas en todas las versiones utilizando las siguientes claves del Registro:  
  
 Web Release 1:  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXMLX\SchemaCacheSize  
```  
  
 SQLXML 2,0:  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXML2\SchemaCacheSize  
```  
  
 SQLXML 3.0:  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXML3\SchemaCacheSize  
```  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteRegistry](../../../includes/ssnoteregistry-md.md)]  
  
 Para obtener más información acerca de la instalación en paralelo, vea [novedades de SQLXML 4,0 SP1](../../sqlxml/what-s-new-in-sqlxml-4-0-sp1.md).  
  
 El almacenamiento de esquemas en la memoria caché mejora significativamente el rendimiento de una consulta XPath. Cuando se ejecuta una consulta XPath para un esquema de asignación, el esquema se almacena en memoria y las estructuras de datos necesarias se generan en memoria. Si se establece el almacenamiento en caché del esquema, el esquema permanece en memoria, con lo que se mejora el rendimiento de las consultas XPath subsiguientes.  
  
 Puede establecer el tamaño de caché para el esquema agregando la clave anterior en el Registro  
  
 El tamaño del esquema se establece en función de la memoria disponible y el número de esquemas que esté utilizando. El tamaño predeterminado de **SchemaCacheSize** es 31. Si establece **SchemaCacheSize** superior, se usa más memoria. Por consiguiente, puede aumentar el tamaño de caché si el acceso al esquema parece lento o puede reducirlo si hay poca memoria.  
  
 Por motivos de rendimiento, se recomienda establecer **SchemaCacheSize** en un valor mayor que el número de esquemas de asignación que se suelen usar. A medida que aumenta el número de esquemas, si **SchemaCacheSize** es menor que el número de esquemas que tiene, el rendimiento se degrada.  
  
> [!NOTE]  
>  Durante el desarrollo, se recomienda que no almacene los esquemas en la memoria caché, ya que los cambios hechos en los esquemas no se reflejan en la caché durante aproximadamente dos minutos.  
  
## <a name="see-also"></a>Consulte también  
 [Almacenamiento en caché de plantillas &#40;SQLXML 4,0&#41;](template-caching-sqlxml-4-0.md)   
 [Almacenamiento en caché XSL &#40;SQLXML 4,0&#41;](xsl-caching-sqlxml-4-0.md)  
  
  
