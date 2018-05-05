---
title: Mensajes devueltos por el controlador ODBC para Oracle | Documentos de Microsoft
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
- error messages [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], error messages
ms.assetid: 150bde1d-adb6-4e77-90e9-4dc93499a746
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0680f839b96bf3a792ce0c4ac16d10ffc9a64f00
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
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
