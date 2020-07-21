---
title: Niveles de cumplimiento de SQL (controlador ODBC para Oracle) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- conformance levels [ODBC], SQL
- SQL conformance levels [ODBC]
- ODBC driver for Oracle [ODBC], conformance levels
ms.assetid: 077a6c6a-2c57-42c9-a4fd-4cf0e65cf7e2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e283bbc13f0d0dda055b047b027f7b9816502df5
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300685"
---
# <a name="sql-conformance-levels-odbc-driver-for-oracle"></a>Niveles de compatibilidad de SQL (controlador ODBC para Oracle)
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 El controlador ODBC para Oracle es compatible con la gramática de SQL mínima y la gramática de SQL básica y también admite las siguientes extensiones ODBC para SQL:  
  
-   Datos de fecha, hora y marca de tiempo  
  
-   Combinaciones externas izquierda y derecha  
  
-   Funciones numéricas:  
  
    |||||  
    |-|-|-|-|  
    |Abs|Log|round|tan|  
    |Ceiling|Log10|second|truncate|  
    |Cos|Mod|Firma||  
    |Exp|Pi|sin||  
    |Floor|Potencia|sqrt||  
  
-   Funciones de fecha:  
  
    |||||  
    |-|-|-|-|  
    |Curdate|DayOfWeek|MonthName|second|  
    |Curtime|Dayofyear|minute|week|  
    |Dayname|Hour|ahora|year|  
    |DayOfMonth|Mes|quarter||  
  
-   Funciones de cadena:  
  
    |||||  
    |-|-|-|-|  
    |Ascii|Left|right|UCase|  
    |Char|Length|RTRIM||  
    |Concat|Ltrim|Soundex||  
    |Lcase|Replace|substring||  
  
-   Función de conversión de tipos:  
  
    ||  
    |-|  
    |Convert|  
  
-   Funciones del sistema:  
  
    ||  
    |-|  
    |Ifnull|  
    |Usuario|
