---
title: Longitud de datos de columna | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- column data [ODBC]
- length of column data [ODBC]
- ODBC cursor library [ODBC], cache
- cursor library [ODBC], cache
- cache [ODBC]
ms.assetid: c762c881-ebe0-4eac-84d5-f30281fc3eca
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6d14fa4303dd1f67a77bf14dcebeeb933ccce9e1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47793643"
---
# <a name="length-of-column-data"></a>Longitud de datos de columna
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite usar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad de cursor del controlador.  
  
 La biblioteca de cursores crea un búfer en la memoria caché para cada búfer de longitud/indicador enlazado para el conjunto de resultados con **SQLBindCol**. Lo utiliza los valores de estos búferes para construir un **donde** cláusula cuando emula posicionada update o delete. Cuando recupera los datos de origen de datos y cuando ejecuta las instrucciones update posicionadas actualiza estos búferes de los búferes de conjunto de filas.  
  
 Si el tipo C de un búfer de datos es SQL_C_CHAR o SQL_C_BINARY y el valor de longitud/indicador es SQL_NTS, la longitud de cadena de los datos se coloca en el búfer de longitud/indicador.  
  
> [!NOTE]  
>  La biblioteca de cursores no actualiza su caché para una columna si **StrLen_or_IndPtr* en el conjunto de filas correspondiente búfer es SQL_DATA_AT_EXEC ni el resultado de la macro SQL_LEN_DATA_AT_EXEC.
