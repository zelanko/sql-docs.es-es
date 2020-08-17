---
description: SQLError (controlador ODBC de Visual FoxPro)
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 09f901b72d292f962076bff2aa521c8214e8f0e7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88340261"
---
# <a name="sqlerror-visual-foxpro-odbc-driver"></a>SQLError (controlador ODBC de Visual FoxPro)
> [!NOTE]  
>  Este tema contiene información específica del controlador ODBC de Visual FoxPro. Para obtener información general sobre esta función, vea el tema correspondiente en referencia de la [API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Compatibilidad: completa  
  
 Conformidad con la API de ODBC: nivel básico  
  
 Devuelve información de error o de estado sobre el último error. El controlador mantiene una pila o lista de errores que se pueden devolver para los argumentos *hstmt*, *hdbc*y *HENV* , en función de cómo se realice la llamada a **SQLError** . La cola de errores se vacía después de cada instrucción.  
  
 En la tabla siguiente se describen los argumentos **SQLError** y los valores devueltos usados por el controlador.  
  
|SQLError (argumento)|Descripción del valor devuelto|  
|-----------------------|------------------------------|  
|*szSQLState*|Valor del SQLSTATE representado por el error.|  
|*pfNativeError*|Un valor distinto de cero indica un [mensaje de error nativo del controlador ODBC de Visual FoxPro](../../odbc/microsoft/visual-foxpro-odbc-driver-native-error-messages.md). Un valor de cero indica que el controlador ha detectado el error y se ha asignado al [código de error de ODBC](../../odbc/microsoft/odbc-error-codes-visual-foxpro-odbc-driver.md)adecuado.|  
|*szErrorMsg*|Texto del error nativo o de ODBC.|  
|*pcbErrorMsg*|La longitud del texto del mensaje más la longitud de los identificadores.|  
  
 Para obtener más información sobre los mensajes de error del controlador, consulte [información general sobre mensajes de error](../../odbc/microsoft/error-messages-visual-foxpro-odbc-driver.md). Para obtener más información sobre esta función, vea [SQLError](../../odbc/reference/syntax/sqlerror-function.md) en la *Referencia del programador de ODBC*.
