---
description: Niveles de compatibilidad de SQL (controlador ODBC para Oracle)
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
ms.openlocfilehash: 78e98aed952ef8b15a4654be9f82e355d1b4177b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483428"
---
# <a name="sql-conformance-levels-odbc-driver-for-oracle"></a>Niveles de compatibilidad de SQL (controlador ODBC para Oracle)
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 El controlador ODBC para Oracle es compatible con la gramática de SQL mínima y la gramática de SQL básica y también admite las siguientes extensiones ODBC para SQL:  
  
-   Datos de fecha, hora y marca de tiempo  
  
-   Combinaciones externas izquierda y derecha  
  
-   Funciones numéricas:  

    :::row:::
        :::column:::
            Abs  
            Ceiling  
            Cos  
            Exp  
            Floor  
        :::column-end:::
        :::column:::
            Log  
            Log10  
            Mod  
            Pi  
            Potencia  
        :::column-end:::
        :::column:::
            round  
            segundo  
            Firma  
            sin  
            sqrt  
        :::column-end:::
        :::column:::
            tan  
            truncate  
        :::column-end:::
    :::row-end:::
    
-   Funciones de fecha:  

    :::row:::
        :::column:::
            Curdate  
            Curtime  
            Dayname  
            DayOfMonth  
        :::column-end:::
        :::column:::
            DayOfWeek  
            Dayofyear  
            Hora  
            Month  
        :::column-end:::
        :::column:::
            MonthName  
            minute  
            ahora  
            quarter  
        :::column-end:::
        :::column:::
            segundo  
            week  
            year  
        :::column-end:::
    :::row-end:::

-   Funciones de cadena:  

    :::row:::
        :::column:::
            Ascii  
            Char  
            Concat  
            Lcase  
        :::column-end:::
        :::column:::
            Left  
            Length  
            Ltrim  
            Replace  
        :::column-end:::
        :::column:::
            right  
            RTRIM  
            Soundex  
            substring  
        :::column-end:::
        :::column:::
            UCase  
        :::column-end:::
    :::row-end:::

-   Función de conversión de tipos:  

    Convert  

-   Funciones del sistema:  
  
    Ifnull  
    Usuario
