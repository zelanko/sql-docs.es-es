---
title: 'Paso 5: Confirmar la transacción ? Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application process [ODBC], committing transactions
- committing transactions [ODBC]
- transaction commit [ODBC]
ms.assetid: 311685e2-f7b5-4ddc-8020-59380cd2f035
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e348ce697e512f30db46d14535cf19bd6d530f61
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283355"
---
# <a name="step-5-commit-the-transaction"></a>Paso 5: Confirmación de la transacción
El siguiente paso es confirmar la transacción, como se muestra en la siguiente ilustración.  
  
 ![Muestra cómo confirmar una transacción](../../../odbc/reference/develop-app/media/pr16.gif "pr16")  
  
 El quinto paso es llamar a **SQLEndTran** para confirmar o revertir la transacción. La aplicación realiza este paso solo si establece el modo de confirmación de transacción en confirmación manual; si el modo de confirmación de transacción es de confirmación automática, que es el valor predeterminado, la transacción se confirma automáticamente cuando se ejecuta la instrucción. Para más información, consulte [Transacciones](../../../odbc/reference/develop-app/transactions-odbc.md).  
  
 Para ejecutar una instrucción en una nueva transacción, la aplicación vuelve al paso 3. Para desconectarse del origen de datos, la aplicación continúa con el paso 6.
