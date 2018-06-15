---
title: Dirección del búfer de datos | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
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
ms.openlocfilehash: 46b961c1820714e79a0d362c187272105e90f656
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32908500"
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
