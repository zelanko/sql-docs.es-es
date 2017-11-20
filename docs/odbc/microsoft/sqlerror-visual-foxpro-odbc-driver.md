---
title: SQLError (controlador ODBC de Visual FoxPro) | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLError function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 8315ec16-1c22-447a-a577-39bd94f61070
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 46696509f9276ac4974604c931c4d77acbaae15b
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqlerror-visual-foxpro-odbc-driver"></a>SQLError (controlador ODBC de Visual FoxPro)
> [!NOTE]  
>  Este tema contiene información específica del controlador ODBC de Visual FoxPro. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Soporte técnico: completo  
  
 Conformidad de la API de ODBC: Nivel de núcleo  
  
 Devuelve información de estado o de error sobre el último error. El controlador mantiene una pila o una lista de errores que se pueden devolver para la *hstmt*, *hdbc*, y *henv* argumentos, dependiendo de cómo la llamada a **SQLError**  se realiza. La cola de errores se vacía después de cada instrucción.  
  
 La tabla siguiente se describen los **SQLError** argumentos y valores devueltos que utiliza el controlador.  
  
|Argumento SQLError|Descripción de valor devuelto|  
|-----------------------|------------------------------|  
|*szSQLState*|El valor para el valor de SQLSTATE representado por el error.|  
|*pfNativeError*|Un valor distinto de cero indica un [Visual FoxPro ODBC Driver nativo mensaje](../../odbc/microsoft/visual-foxpro-odbc-driver-native-error-messages.md). Un valor de cero indica que el error ha sido detectado por el controlador y se ha asignado a la correspondiente [código de Error de ODBC](../../odbc/microsoft/odbc-error-codes-visual-foxpro-odbc-driver.md).|  
|*szErrorMsg*|El texto del error nativo o error de ODBC.|  
|*pcbErrorMsg*|La longitud del texto del mensaje más la longitud de los identificadores.|  
  
 Para obtener más información sobre mensajes de error de controlador, consulte [información general de los mensajes de Error](../../odbc/microsoft/error-messages-visual-foxpro-odbc-driver.md). Para obtener más información acerca de esta función, consulte [SQLError](../../odbc/reference/syntax/sqlerror-function.md) en el *referencia del programador de ODBC*.

