---
title: Mensajes devueltos por el controlador ODBC para Oracle | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- error messages [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], error messages
ms.assetid: 150bde1d-adb6-4e77-90e9-4dc93499a746
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3245479e44892d51d51027693e1231073d11c226
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="messages-returned-by-the-odbc-driver-for-oracle"></a>Mensajes devueltos por el controlador ODBC para Oracle
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 Si un mensaje de error de Oracle está disponible, se le devolverá precedidos por el [Microsoft] [controlador ODBC para Oracle] y [Oracle] etiquetas; en caso contrario, se devuelve el mensaje sin la etiqueta [Oracle] como en los ejemplos siguientes:  
  
## <a name="oracle-error-message"></a>Mensaje de error de Oracle:  
  
```  
[Microsoft][ODBC driver for Oracle][Oracle]ORA-nnnnn message-text  
```  
  
## <a name="odbc-driver-for-oracle-error-message"></a>Controlador ODBC para el mensaje de error de Oracle:  
  
```  
[Microsoft][ODBC driver for Oracle]  
```
