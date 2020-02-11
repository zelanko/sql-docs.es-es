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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7cd157edd6111dec29ae238a1c383879e66ac0b3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68067431"
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
