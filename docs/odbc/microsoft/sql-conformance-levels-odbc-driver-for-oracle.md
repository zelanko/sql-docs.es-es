---
title: Niveles de compatibilidad de SQL (controlador ODBC para Oracle) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 241f4f3da12f63c15d917a0e47cb13ad0e96e6e3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68063356"
---
# <a name="sql-conformance-levels-odbc-driver-for-oracle"></a>Niveles de compatibilidad de SQL (controlador ODBC para Oracle)
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, use el controlador ODBC proporcionado por Oracle.  
  
 El controlador ODBC para Oracle admite la gramática mínima de SQL y la gramática básica de SQL y también admite las siguientes extensiones ODBC a SQL:  
  
-   Datos de fecha, hora y marca de tiempo  
  
-   Izquierda y combinaciones externas derechas  
  
-   Funciones numéricas:  
  
    |||||  
    |-|-|-|-|  
    |Abs|Registro|round|tan|  
    |límite superior|LOG10|second|truncate|  
    |Cos|Mod|inicio de sesión||  
    |Exp|PI|sin||  
    |Floor|Power|sqrt||  
  
-   Funciones de fecha:  
  
    |||||  
    |-|-|-|-|  
    |CURDATE|DayOfWeek|MonthName|second|  
    |Curtime|Dayofyear|minute|week|  
    |Dayname|Hour|ahora|year|  
    |DayOfMonth|Mes|Trimestre||  
  
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
