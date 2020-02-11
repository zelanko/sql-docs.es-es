---
title: Mensajes devueltos por el controlador ODBC para Oracle | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- error messages [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], error messages
ms.assetid: 150bde1d-adb6-4e77-90e9-4dc93499a746
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bb2fc54692a77441bb2516ad72c0c44951152f56
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68045181"
---
# <a name="messages-returned-by-the-odbc-driver-for-oracle"></a>Mensajes devueltos por el controlador ODBC para Oracle
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 Si hay un mensaje de error de Oracle disponible, se devolverá precedido por las etiquetas [Microsoft], [ODBC driver for Oracle] y [Oracle]; de lo contrario, el mensaje se devuelve sin la etiqueta [Oracle] como en los ejemplos siguientes:  
  
## <a name="oracle-error-message"></a>Mensaje de error de Oracle:  
  
```  
[Microsoft][ODBC driver for Oracle][Oracle]ORA-nnnnn message-text  
```  
  
## <a name="odbc-driver-for-oracle-error-message"></a>Mensaje de error del controlador ODBC para Oracle:  
  
```  
[Microsoft][ODBC driver for Oracle]  
```
