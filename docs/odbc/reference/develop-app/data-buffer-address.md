---
title: Dirección de búfer de datos | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305276"
---
# <a name="data-buffer-address"></a>Dirección del búfer de datos
La aplicación pasa la dirección del búfer de datos al controlador en un argumento, a menudo denominado *ValuePtr* o un nombre similar. Por ejemplo, en la siguiente llamada a **SQLBindCol**, la aplicación especifica la dirección de la variable de *fecha* :  
  
```  
SQL_DATE_STRUCT Date;  
SQLINTEGER DateInd;  
SQLBindCol(hstmt, 1, SQL_C_TYPE_DATE, &dsDate, 0, &DateInd);  
```  
  
 Como se mencionó en la sección [asignación y liberación de búferes](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md) , la dirección de un búfer diferido debe ser válida hasta que se desenlace el búfer.  
  
 A menos que esté específicamente prohibida, la dirección de un búfer de datos puede ser un puntero nulo. En el caso de los búferes que se usan para enviar datos al controlador, esto hace que el controlador ignore la información contenida normalmente en el búfer. En el caso de los búferes usados para recuperar datos del controlador, esto hace que el controlador no devuelva un valor. En ambos casos, el controlador omite el argumento de longitud de búfer de datos correspondiente.
