---
title: Niveles de compatibilidad de SQL (controlador ODBC para Oracle) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- conformance levels [ODBC], SQL
- SQL conformance levels [ODBC]
- ODBC driver for Oracle [ODBC], conformance levels
ms.assetid: 077a6c6a-2c57-42c9-a4fd-4cf0e65cf7e2
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 247009b387cf7538a841477bab5f7be72fa20fd5
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sql-conformance-levels-odbc-driver-for-oracle"></a>Niveles de compatibilidad de SQL (controlador ODBC para Oracle)
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 El controlador ODBC para Oracle admite la gramática mínima de SQL y la gramática básica de SQL y también admite las siguientes extensiones ODBC para SQL:  
  
-   Datos de fecha, hora y marca de tiempo  
  
-   Izquierda y combinaciones externas derechas  
  
-   Funciones numéricas:  
  
    |||||  
    |-|-|-|-|  
    |Abs|Log|round|tan|  
    |Límite superior|LOG10|second|truncate|  
    |Cos|Mod|Inicio de sesión||  
    |Exp|PI|sin||  
    |Floor|Power|sqrt||  
  
-   Funciones de fecha:  
  
    |||||  
    |-|-|-|-|  
    |CURDATE|DayOfWeek|MonthName|second|  
    |Curtime|Dayofyear|minute|week|  
    |Dayname|Hour|ahora|year|  
    |DayOfMonth|Month|Trimestre||  
  
-   Funciones de cadena:  
  
    |||||  
    |-|-|-|-|  
    |ASCII|Izquierda|Correcto|UCase|  
    |Char|Longitud|RTrim||  
    |Concat|Ltrim|SOUNDEX||  
    |Lcase|Reemplazar|substring||  
  
-   Función de conversión de tipos:  
  
    ||  
    |-|  
    |Convertir|  
  
-   Funciones del sistema:  
  
    ||  
    |-|  
    |Ifnull|  
    |Usuario|
