---
title: Dirección del búfer de datos (Data Buffer Address) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- address of data buffers [ODBC]
- buffers [ODBC], data
- data buffers [ODBC], address
ms.assetid: f2426d68-71bc-4ef7-a5cb-ee9d6c1c9671
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 578e4e37a78818cb640d9f32e2480cec5951df63
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305276"
---
# <a name="data-buffer-address"></a>Dirección del búfer de datos
La aplicación pasa la dirección del búfer de datos al controlador en un argumento, a menudo denominado *ValuePtr* o un nombre similar. Por ejemplo, en la siguiente llamada a **SQLBindCol**, la aplicación especifica la dirección de la variable *Date:*  
  
```  
SQL_DATE_STRUCT Date;  
SQLINTEGER DateInd;  
SQLBindCol(hstmt, 1, SQL_C_TYPE_DATE, &dsDate, 0, &DateInd);  
```  
  
 Como se mencionó en la sección [Asignación y liberación de búferes,](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md) la dirección de un búfer diferido debe seguir siendo válida hasta que el búfer esté desenlazado.  
  
 A menos que esté específicamente prohibido, la dirección de un búfer de datos puede ser un puntero nulo. Para los búferes utilizados para enviar datos al controlador, esto hace que el controlador ignore la información normalmente contenida en el búfer. Para los búferes utilizados para recuperar datos del controlador, esto hace que el controlador no devuelva un valor. En ambos casos, el controlador omite el argumento de longitud del búfer de datos correspondiente.
