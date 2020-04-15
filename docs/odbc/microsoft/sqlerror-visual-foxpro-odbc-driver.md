---
title: SQLError (Controlador ODBC de Visual FoxPro) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0d1247217905187cfb2dbaca6d7b7b562d0175bd
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298685"
---
# <a name="sqlerror-visual-foxpro-odbc-driver"></a>SQLError (controlador ODBC de Visual FoxPro)
> [!NOTE]  
>  Este tema contiene información específica del controlador ODBC de Visual FoxPro. Para obtener información general sobre esta función, consulte el tema adecuado en Referencia de [la API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Soporte: Completo  
  
 Conformidad de la API ODBC: nivel principal  
  
 Devuelve información de error o estado sobre el último error. El controlador mantiene una pila o una lista de errores que se pueden devolver para los argumentos *hstmt*, *hdbc*y *henv,* dependiendo de cómo se realice la llamada a **SQLError.** La cola de errores se vacía después de cada instrucción.  
  
 En la tabla siguiente se describen los argumentos **SQLError** y los valores devueltos utilizados por el controlador.  
  
|Argumento SQLError|Descripción del valor devuelto|  
|-----------------------|------------------------------|  
|*szSQLState*|El valor de SQLSTATE representado por el error.|  
|*pfNativeError*|Un valor distinto de cero indica un mensaje de error nativo del controlador ODBC de [Visual FoxPro.](../../odbc/microsoft/visual-foxpro-odbc-driver-native-error-messages.md) Un valor de cero indica que el controlador ha detectado el error y se ha asignado al código de [error ODBC](../../odbc/microsoft/odbc-error-codes-visual-foxpro-odbc-driver.md)adecuado.|  
|*szErrorMsg*|El texto del error nativo o del error ODBC.|  
|*pcbErrorMsg*|La longitud del texto del mensaje más la longitud de los identificadores.|  
  
 Para obtener más información sobre los mensajes de error del controlador, vea [Información general sobre mensajes](../../odbc/microsoft/error-messages-visual-foxpro-odbc-driver.md)de error . Para obtener más información acerca de esta función, vea [SQLError](../../odbc/reference/syntax/sqlerror-function.md) en la *referencia del programador ODBC*.
