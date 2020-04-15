---
title: Mensajes devueltos por el controlador ODBC para Oracle ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b8bdaf4238bd220987364a77aaa1af837885c6e6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298865"
---
# <a name="messages-returned-by-the-odbc-driver-for-oracle"></a>Mensajes devueltos por el controlador ODBC para Oracle
> [!IMPORTANT]  
>  Esta característica se eliminará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 Si hay un mensaje de error de Oracle disponible, se devolverá precedido por las etiquetas [Microsoft], [ODBC Driver for Oracle] y [Oracle]; de lo contrario, el mensaje se devuelve sin la etiqueta [Oracle] como en los siguientes ejemplos:  
  
## <a name="oracle-error-message"></a>Mensaje de error de Oracle:  
  
```  
[Microsoft][ODBC driver for Oracle][Oracle]ORA-nnnnn message-text  
```  
  
## <a name="odbc-driver-for-oracle-error-message"></a>Mensaje de error del controlador ODBC para Oracle:  
  
```  
[Microsoft][ODBC driver for Oracle]  
```
