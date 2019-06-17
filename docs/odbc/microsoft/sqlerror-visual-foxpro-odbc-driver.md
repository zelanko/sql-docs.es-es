---
title: SQLError (controlador ODBC de Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLError function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 8315ec16-1c22-447a-a577-39bd94f61070
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3014c5c2af1a0ef8e5f485c790089e4807834446
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63313277"
---
# <a name="sqlerror-visual-foxpro-odbc-driver"></a>SQLError (controlador ODBC de Visual FoxPro)
> [!NOTE]  
>  Este tema contiene información específica del controlador ODBC de Visual FoxPro. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Soporte técnico: Completo  
  
 Conformidad de la API de ODBC: Nivel básico  
  
 Devuelve información de estado o de error sobre el último error. El controlador mantiene una pila o una lista de errores que se pueden devolver para el *hstmt*, *hdbc*, y *henv* argumentos, dependiendo de cómo la llamada a **SQLError**  se realiza. La cola de errores se vacíe después de cada instrucción.  
  
 La tabla siguiente se describen los **SQLError** argumentos y valores devueltos que utiliza el controlador.  
  
|Argumento de SQLError|Descripción del valor devuelto|  
|-----------------------|------------------------------|  
|*szSQLState*|El valor de SQLSTATE representado por el error.|  
|*pfNativeError*|Un valor distinto de cero indica un [Visual FoxPro ODBC Driver nativo mensaje](../../odbc/microsoft/visual-foxpro-odbc-driver-native-error-messages.md). Un valor de cero indica el error ha sido detectado por el controlador y asigna a la correspondiente [código de Error de ODBC](../../odbc/microsoft/odbc-error-codes-visual-foxpro-odbc-driver.md).|  
|*szErrorMsg*|El texto del error nativo o un error de ODBC.|  
|*pcbErrorMsg*|La longitud del texto del mensaje así como la longitud de los identificadores.|  
  
 Para obtener más información sobre los mensajes de error de controlador, consulte [información general de los mensajes de Error](../../odbc/microsoft/error-messages-visual-foxpro-odbc-driver.md). Para obtener más información acerca de esta función, vea [SQLError](../../odbc/reference/syntax/sqlerror-function.md) en el *referencia del programador de ODBC*.
