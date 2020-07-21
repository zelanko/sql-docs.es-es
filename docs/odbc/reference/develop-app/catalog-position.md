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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0305d978dc4ecd21892a0be3916fa5072b7be95a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81303386"
---
# <a name="catalog-position"></a>Posición del catálogo
La posición de un nombre de catálogo en un identificador y cómo se separa del resto del identificador varía del origen de datos al origen de datos. Por ejemplo, en un origen de datos xBase, el nombre del catálogo es un directorio y, en Microsoft® Windows®, se separa del nombre de la tabla (que es un nombre de archivo) mediante\\una barra diagonal inversa (). En la ilustración siguiente se muestra esta condición.  
  
 ![Posición del catálogo: Xbase](../../../odbc/reference/develop-app/media/ch0801.gif "ch0801")  
  
 En un origen de datos de SQL Server, el catálogo es una base de datos y se separa de los nombres de tabla y esquema por un punto (.).  
  
 ![Posición del catálogo: SQL Server](../../../odbc/reference/develop-app/media/ch0802.gif "ch0802")  
  
 En un origen de datos de Oracle, el catálogo también es la base de datos pero sigue el nombre de la tabla y se separa de los nombres de esquema y tabla mediante un signo de arroba (@).  
  
 ![Posición del catálogo: Oracle](../../../odbc/reference/develop-app/media/ch0803.gif "ch0803")  
  
 Para determinar el separador de catálogo y la ubicación del nombre del catálogo, una aplicación llama a **SQLGetInfo** con las opciones SQL_CATALOG_NAME_SEPARATOR y SQL_CATALOG_LOCATION. Las aplicaciones interoperables deben construir identificadores según estos valores.  
  
 Cuando se comillas de los identificadores que contienen más de una parte, las aplicaciones deben tener cuidado de citar cada parte por separado y no citar el carácter que separa los identificadores. Por ejemplo, la siguiente instrucción para seleccionar todas las filas y columnas de una tabla xBase va entre comillas de los nombres de catálogo (\XBASE\SALES\CORP) y tabla (Parts. dbf), pero no\\el separador de catálogo ():  
  
```  
SELECT * FROM "\XBASE\SALES\CORP"\"PARTS.DBF"  
```  
  
 La instrucción siguiente para seleccionar todas las filas y columnas de una tabla de Oracle cotiza los nombres de catálogo (ventas), esquema (corporativo) y tabla (partes), pero no los separadores de catálogo (@) o esquema (.):  
  
```  
SELECT * FROM "Corporate"."Parts"@"Sales"  
```  
  
 Para obtener información sobre los identificadores de Comillas, vea la sección siguiente, [identificadores entrecomillados](../../../odbc/reference/develop-app/quoted-identifiers.md).
