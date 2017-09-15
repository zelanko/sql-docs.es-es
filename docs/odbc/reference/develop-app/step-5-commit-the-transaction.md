---
title: "Paso 5: Confirmar la transacción | Documentos de Microsoft"
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
- application process [ODBC], committing transactions
- committing transactions [ODBC]
- transaction commit [ODBC]
ms.assetid: 311685e2-f7b5-4ddc-8020-59380cd2f035
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9ac53209063a1204b57e7183501b5901dc8ea248
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="step-5-commit-the-transaction"></a>Paso 5: Confirmar la transacción
El siguiente paso es confirmar la transacción, tal como se muestra en la siguiente ilustración.  
  
 ![Muestra cómo confirmar una transacción](../../../odbc/reference/develop-app/media/pr16.gif "pr16")  
  
 El quinto paso consiste en llamar a **SQLEndTran** para confirmar o revertir la transacción. La aplicación realiza este paso solo si establece el modo de confirmación de transacción en la confirmación manual; Si el modo de confirmación de transacción es confirmación automática, que es el valor predeterminado, la transacción se confirman automáticamente cuando se ejecuta la instrucción. Para obtener más información, consulte [transacciones](../../../odbc/reference/develop-app/transactions-odbc.md).  
  
 Para ejecutar una instrucción en una nueva transacción, la aplicación vuelve al paso 3. Para desconectarse del origen de datos, la aplicación continúa con el paso 6.
