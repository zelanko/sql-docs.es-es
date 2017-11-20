---
title: Llamar a SQLSetPos | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- compatibility [ODBC], SQLSetPos
- SQLSetPos function [ODBC], calling
- upgrading applications [ODBC], SQLSetPos
- backward compatibility [ODBC], SqlSetPos
- application upgrades [ODBC], SQLSetPos
ms.assetid: 846354b8-966c-4c2c-b32f-b0c8e649cedd
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 434031a496faae19ee37b8273341cc0ede6d0313
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="calling-sqlsetpos"></a>Llamar a SQLSetPos
En ODBC 2. *x*, el puntero a la matriz de estado de fila se encontraba argumento pasado a **SQLExtendedFetch**. La matriz de Estados de fila se actualizó más adelante mediante una llamada a **SQLSetPos**. Algunos controladores se basaban en el hecho de que esta matriz no cambia entre **SQLExtendedFetch** y **SQLSetPos**. En ODBC 3. *x*, el puntero a la matriz de estado es un campo de descriptor y, por tanto, la aplicación puede cambiar fácilmente para que apunte a una matriz distinta. Esto puede ser un problema cuando una aplicación ODBC 3. *x* aplicación está trabajando con una API ODBC 2. *x* controlador pero está llamando a **SQLSetStmtAttr** para establecer el puntero de estado de la matriz y llama a **SQLFetchScroll** para capturar los datos. El Administrador de controladores se asigna como una secuencia de llamadas a **SQLExtendedFetch**. En el código siguiente, producirá un error haría normalmente cuando el Administrador de controladores se asigna el segundo **SQLSetStmtAttr** llamar cuando se trabaja con una API ODBC 2*.x* controlador:  
  
```  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, rgfRowStatus, 0);  
SQLFetchScroll(hstmt, fFetchType, iRow);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, rgfRowStat1, 0);  
SQLSetPos(hstmt, iRow, fOption, fLock);  
```  
  
 Se generará el error si no hubiera ninguna manera de cambiar el puntero de estado de fila en ODBC 2. *x* entre las llamadas a **SQLExtendedFetch**. En su lugar, el Administrador de controladores realiza los pasos siguientes cuando se trabaja con una API ODBC 2*.x* controlador:  
  
1.  Inicializa un marcador interno del Administrador de controladores *fSetPosError* en TRUE.  
  
2.  Cuando una aplicación llama **SQLFetchScroll**, Establece el Administrador de controladores *fSetPosError* en FALSE.  
  
3.  Cuando la aplicación llama **SQLSetStmtAttr** para establecer SQL_ATTR_ROW_STATUS_PTR, Establece el Administrador de controladores *fSetPosError* toTRUE igual.  
  
4.  Cuando la aplicación llama **SQLSetPos**, con *fSetPosError* igual a TRUE, el Administrador de controladores genera SQL_ERROR con SQLSTATE HY011 (atributo no se puede establecer ahora) para indicar que la aplicación intentó llamar a **SQLSetPos** después de cambiar el puntero de estado de fila, pero antes de llamar a **SQLFetchScroll**.

