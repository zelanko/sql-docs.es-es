---
title: Posición del catálogo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], catalog position
- catalog position [ODBC]
ms.assetid: 5bc5f64b-c75a-43d2-8745-102ec7a49000
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 22a9a9d50891a6101076af6378fb33543274b21b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63237949"
---
# <a name="catalog-position"></a>Posición del catálogo
La posición de un nombre de catálogo en un identificador y cómo lo está separado del resto del identificador varía en función del origen de datos al origen de datos. Por ejemplo, en un origen de datos de Xbase, el nombre del catálogo es un directorio y, en Microsoft® Windows®, se separa del nombre de tabla (que es un nombre de archivo) por una barra diagonal inversa (\\). La siguiente ilustración muestra esta condición.  
  
 ![Posición del catálogo: Xbase](../../../odbc/reference/develop-app/media/ch0801.gif "ch0801")  
  
 En un origen de datos de SQL Server, el catálogo es una base de datos y se separa de los nombres de esquema y tabla por un punto (.).  
  
 ![Posición del catálogo: SQL Server](../../../odbc/reference/develop-app/media/ch0802.gif "ch0802")  
  
 En un origen de datos de Oracle, el catálogo también es la base de datos, pero sigue el nombre de tabla y se separa de los nombres de esquema y tabla con una arroba (@).  
  
 ![Posición del catálogo: Oracle](../../../odbc/reference/develop-app/media/ch0803.gif "ch0803")  
  
 Para determinar el separador del catálogo y la ubicación del nombre del catálogo, llama una aplicación **SQLGetInfo** con las opciones SQL_CATALOG_NAME_SEPARATOR y SQL_CATALOG_LOCATION. Aplicaciones interoperables deben construir los identificadores de acuerdo con estos valores.  
  
 Al entrecomillar los identificadores que contienen más de una parte, las aplicaciones deben tener cuidadas a la oferta por separado cada parte y no el carácter que separa los identificadores de comillas. Por ejemplo, la instrucción siguiente para seleccionar todas las filas y columnas de una tabla de Xbase ofertas del catálogo (\XBASE\SALES\CORP) y los nombres de tabla (Parts.dbf), pero no el separador del catálogo (\\):  
  
```  
SELECT * FROM "\XBASE\SALES\CORP"\"PARTS.DBF"  
```  
  
 El catálogo (ventas), el esquema (corporativo) y los nombres de tabla (elementos), pero no en el catálogo de ofertas de la instrucción siguiente para seleccionar todas las filas y columnas de una tabla de Oracle (@) o separadores de esquema (.):  
  
```  
SELECT * FROM "Corporate"."Parts"@"Sales"  
```  
  
 Para obtener información acerca de los identificadores de comillas, vea la sección siguiente, [identificadores entre comillas](../../../odbc/reference/develop-app/quoted-identifiers.md).
