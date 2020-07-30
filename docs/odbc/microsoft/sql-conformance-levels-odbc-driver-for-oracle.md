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
ms.openlocfilehash: 969296e377d398615ad95cf1337c3f9f97d5eb5c
ms.sourcegitcommit: 99f61724de5edf6640efd99916d464172eb23f92
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/28/2020
ms.locfileid: "87363405"
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
            Energía  
        :::column-end:::
        :::column:::
            round  
            second  
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
            second  
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
