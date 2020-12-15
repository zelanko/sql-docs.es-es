---
title: Almacenamiento en caché de esquemas (SQLXML)
description: Aprenda a usar las claves del registro para controlar explícitamente el almacenamiento en caché de esquemas y mejorar el rendimiento de una consulta XPath en SQLXML 4,0.
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
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
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2e92d3e4f6e22650f702c4076b014441e49bcb38
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97479266"
---
# <a name="schema-caching-sqlxml-40"></a>Almacenamiento de esquemas en caché (SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
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
  
 Para obtener más información acerca de la instalación en paralelo, vea [novedades de SQLXML 4,0 SP1](../../../relational-databases/sqlxml/what-s-new-in-sqlxml-4-0-sp1.md).  
  
 El almacenamiento de esquemas en la memoria caché mejora significativamente el rendimiento de una consulta XPath. Cuando se ejecuta una consulta XPath para un esquema de asignación, el esquema se almacena en memoria y las estructuras de datos necesarias se generan en memoria. Si se establece el almacenamiento en caché del esquema, el esquema permanece en memoria, con lo que se mejora el rendimiento de las consultas XPath subsiguientes.  
  
 Puede establecer el tamaño de caché para el esquema agregando la clave anterior en el Registro  
  
 El tamaño del esquema se establece en función de la memoria disponible y el número de esquemas que esté utilizando. El tamaño predeterminado de **SchemaCacheSize** es 31. Si establece **SchemaCacheSize** superior, se usa más memoria. Por consiguiente, puede aumentar el tamaño de caché si el acceso al esquema parece lento o puede reducirlo si hay poca memoria.  
  
 Por motivos de rendimiento, se recomienda establecer **SchemaCacheSize** en un valor mayor que el número de esquemas de asignación que se suelen usar. A medida que aumenta el número de esquemas, si **SchemaCacheSize** es menor que el número de esquemas que tiene, el rendimiento se degrada.  
  
> [!NOTE]  
>  Durante el desarrollo, se recomienda que no almacene los esquemas en la memoria caché, ya que los cambios hechos en los esquemas no se reflejan en la caché durante aproximadamente dos minutos.  
  
## <a name="see-also"></a>Consulte también  
 [Almacenamiento en caché de plantillas &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/template-caching-sqlxml-4-0.md)   
 [Almacenamiento en caché XSL &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/xsl-caching-sqlxml-4-0.md)  
  
  
