---
title: "Posición del catálogo | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], catalog position
- catalog position [ODBC]
ms.assetid: 5bc5f64b-c75a-43d2-8745-102ec7a49000
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f6b8bf58c2d8db8cf394e6017a9e817c1f20096e
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="catalog-position"></a>Posición del catálogo
La posición de un nombre de catálogo en un identificador y cómo está separada del resto del identificador varía en función del origen de datos al origen de datos. Por ejemplo, en un origen de datos Xbase, el nombre del catálogo es un directorio y, en Microsoft® Windows®, se separa del nombre de tabla (que es un nombre de archivo) por una barra diagonal inversa (\\). En la siguiente ilustración se muestra esta condición.  
  
 ![Posición del catálogo: Xbase](../../../odbc/reference/develop-app/media/ch0801.gif "ch0801")  
  
 En un origen de datos de SQL Server, el catálogo es una base de datos y se separa de los nombres de tabla y un esquema con un punto (.).  
  
 ![Posición del catálogo: SQL Server](../../../odbc/reference/develop-app/media/ch0802.gif "ch0802")  
  
 En un origen de datos de Oracle, el catálogo también es la base de datos pero sigue al nombre de tabla y se separa de los nombres de tabla y un esquema con un signo de arroba (@).  
  
 ![Posición del catálogo: Oracle](../../../odbc/reference/develop-app/media/ch0803.gif "ch0803")  
  
 Para determinar el separador del catálogo y la ubicación del nombre del catálogo, llama a una aplicación **SQLGetInfo** con las opciones SQL_CATALOG_NAME_SEPARATOR y SQL_CATALOG_LOCATION. Aplicaciones interoperables deben construir identificadores según estos valores.  
  
 Al entrecomillar los identificadores que contienen más de una parte, las aplicaciones deben tener cuidadas entrecomillar cada elemento por separado y no entrecomillar el carácter que separa los identificadores. Por ejemplo, la siguiente instrucción para seleccionar todas las filas y columnas de una tabla Xbase proporciona el catálogo (\XBASE\SALES\CORP) y nombres de tabla (Parts.dbf), pero no el separador del catálogo (\\):  
  
```  
SELECT * FROM "\XBASE\SALES\CORP"\"PARTS.DBF"  
```  
  
 La siguiente instrucción para seleccionar todas las filas y columnas de una tabla de Oracle proporciona el catálogo (Sales), esquema (corporativos) y los nombres de tabla (elementos), pero no el catálogo (@) o separadores de esquema (.):  
  
```  
SELECT * FROM "Corporate"."Parts"@"Sales"  
```  
  
 Para obtener información acerca de los identificadores de comillas, vea la sección siguiente, [identificadores entrecomillados](../../../odbc/reference/develop-app/quoted-identifiers.md).
