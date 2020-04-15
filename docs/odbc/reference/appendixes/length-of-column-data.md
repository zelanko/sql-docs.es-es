---
title: Longitud de los datos de la columna ( Column Data) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d0b7ad515661cce4c5b1d407be768cc3da131bb4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304936"
---
# <a name="length-of-column-data"></a>Longitud de datos de columna
> [!IMPORTANT]  
>  Esta característica se eliminará en una versión futura de Windows. Evite usar esta característica en el nuevo trabajo de desarrollo y planee modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad del cursor del controlador.  
  
 La biblioteca de cursores crea un búfer en la memoria caché para cada búfer de longitud/indicador enlazado al conjunto de resultados con **SQLBindCol**. Utiliza los valores de estos búferes para construir una cláusula **WHERE** cuando emula instrucciones de actualización o eliminación posicionadas. Actualiza estos búferes desde los búferes del conjunto de filas cuando recupera datos del origen de datos y cuando ejecuta instrucciones de actualización posicionadas.  
  
 Si el tipo C de un búfer de datos es SQL_C_CHAR o SQL_C_BINARY y el valor de longitud/indicador es SQL_NTS, la longitud de la cadena de los datos se coloca en el búfer de longitud/indicador.  
  
> [!NOTE]  
>  La biblioteca de cursores no actualiza su caché para una columna si **StrLen_or_IndPtr* en el búfer de conjunto de filas correspondiente es SQL_DATA_AT_EXEC o el resultado de la macro SQL_LEN_DATA_AT_EXEC.
