---
title: Dirección del búfer de datos | Documentos de Microsoft
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
- address of data buffers [ODBC]
- buffers [ODBC], data
- data buffers [ODBC], address
ms.assetid: f2426d68-71bc-4ef7-a5cb-ee9d6c1c9671
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fbf649d075f0a28f3d488d5ccde11de9680ffb9e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="data-buffer-address"></a>Dirección del búfer de datos
La aplicación pasa la dirección del búfer de datos para el controlador de un argumento, a menudo denominado *ValuePtr* o un nombre similar. Por ejemplo, en la siguiente llamada a **SQLBindCol**, la aplicación especifica la dirección de la *fecha* variable:  
  
```  
SQL_DATE_STRUCT Date;  
SQLINTEGER DateInd;  
SQLBindCol(hstmt, 1, SQL_C_TYPE_DATE, &dsDate, 0, &DateInd);  
```  
  
 Como se mencionó en la [asignar y liberar búferes](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md) sección, la dirección de un búfer aplazada debe seguir siendo válida hasta que el búfer no está enlazado.  
  
 A menos que específicamente está prohibido, la dirección de un búfer de datos puede ser un puntero nulo. Para los búferes que se utiliza para enviar datos al controlador, esto hace que el controlador pasar por alto la información de contenido normalmente en el búfer. Para los búferes que se utiliza para recuperar datos desde el controlador, esto hace que el controlador no devuelve ningún valor. En ambos casos, el controlador omite el argumento de longitud de búfer de datos correspondiente.
