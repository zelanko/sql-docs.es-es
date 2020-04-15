---
title: Posición del catálogo ( Catalog Position) Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303386"
---
# <a name="catalog-position"></a>Posición del catálogo
La posición de un nombre de catálogo en un identificador y cómo se separa del resto del identificador varía de un origen de datos a un origen de datos. Por ejemplo, en un origen de datos Xbase, el nombre del catálogo es un directorio y, en Microsoft® Windows®, está separado del nombre de tabla (que es un nombre de archivo) mediante una barra diagonal inversa (\\). En la siguiente ilustración se muestra esta condición.  
  
 ![Posición del catálogo: Xbase](../../../odbc/reference/develop-app/media/ch0801.gif "ch0801")  
  
 En un origen de datos de SQL ServerSQL Server , el catálogo es una base de datos y está separado del esquema y los nombres de tabla por un punto (.).  
  
 ![Posición del catálogo: SQL Server](../../../odbc/reference/develop-app/media/ch0802.gif "ch0802")  
  
 En un origen de datos de Oracle, el catálogo también es la base de datos, pero sigue el nombre de la tabla y está separado del esquema y los nombres de tabla por un signo de ar.  
  
 ![Posición del catálogo: Oracle](../../../odbc/reference/develop-app/media/ch0803.gif "ch0803")  
  
 Para determinar el separador de catálogo y la ubicación del nombre del catálogo, una aplicación llama a **SQLGetInfo** con las opciones SQL_CATALOG_NAME_SEPARATOR y SQL_CATALOG_LOCATION. Las aplicaciones interoperables deben construir identificadores según estos valores.  
  
 Al citar identificadores que contienen más de una parte, las aplicaciones deben tener cuidado de citar cada parte por separado y no citar el carácter que separa los identificadores. Por ejemplo, la siguiente instrucción para seleccionar todas las filas y columnas de una tabla Xbase hace referencia a los nombres de\\catálogo (-XBASE-SALES-CORP) y de la tabla (Parts.dbf), pero no con el separador de catálogo ( ):  
  
```  
SELECT * FROM "\XBASE\SALES\CORP"\"PARTS.DBF"  
```  
  
 La siguiente instrucción para seleccionar todas las filas y columnas de una tabla de Oracle cita los nombres de catálogo (Ventas), esquema (corporativo) y tabla (piezas), pero no los separadores de catálogo (o esquema (.):  
  
```  
SELECT * FROM "Corporate"."Parts"@"Sales"  
```  
  
 Para obtener información sobre la cita de identificadores, consulte la sección siguiente, [Identificadores entrecomillados](../../../odbc/reference/develop-app/quoted-identifiers.md).
