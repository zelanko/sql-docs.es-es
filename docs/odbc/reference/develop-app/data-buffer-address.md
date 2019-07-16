---
title: Dirección del búfer de datos | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7cd157edd6111dec29ae238a1c383879e66ac0b3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68067431"
---
# <a name="data-buffer-address"></a>Dirección del búfer de datos
La aplicación pasa la dirección del búfer de datos para el controlador en un argumento, a menudo denominado *ValuePtr* o un nombre similar. Por ejemplo, en la siguiente llamada a **SQLBindCol**, la aplicación especifica la dirección de la *fecha* variable:  
  
```  
SQL_DATE_STRUCT Date;  
SQLINTEGER DateInd;  
SQLBindCol(hstmt, 1, SQL_C_TYPE_DATE, &dsDate, 0, &DateInd);  
```  
  
 Como se mencionó en el [asignar y liberar búferes](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md) sección, la dirección de un búfer aplazada debe seguir siendo válida hasta que el búfer es independiente.  
  
 A menos que se prohíbe en concreto, la dirección de un búfer de datos puede ser un puntero nulo. Para los búferes que utiliza para enviar datos al controlador, esto hace que el controlador pasar por alto la información normalmente contenida en el búfer. Para los búferes se utiliza para recuperar datos desde el controlador, esto hace que el controlador no devuelve ningún valor. En ambos casos, el controlador omite el argumento de longitud de búfer de datos correspondiente.
