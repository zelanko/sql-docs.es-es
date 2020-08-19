---
description: Confirmar y revertir las transacciones
title: Confirmar y revertir transacciones | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- rolling back transactions [ODBC]
- committing transactions [ODBC]
- transactions [ODBC], rolling back
- transactions [ODBC], committing
ms.assetid: 800f2c1a-6f79-4ed1-830b-aa1a62ff5165
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b84be4d2734d9485748351c99ff2675bf3b54213
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424847"
---
# <a name="committing-and-rolling-back-transactions"></a>Confirmar y revertir las transacciones
Para confirmar o revertir una transacción en el modo de confirmación manual, una aplicación llama a **SQLEndTran**. Los controladores para DBMS que admiten transacciones normalmente implementan esta función mediante la ejecución de una instrucción **commit** o **Rollback** . El administrador de controladores no llama a **SQLEndTran** cuando la conexión está en modo de confirmación automática; simplemente devuelve SQL_SUCCESS, incluso si la aplicación intenta revertir la transacción. Dado que los controladores para DBMS que no admiten transacciones siempre están en modo de confirmación automática, pueden implementar **SQLEndTran** para devolver SQL_SUCCESS sin hacer nada o no implementarlo en absoluto.  
  
> [!NOTE]  
>  Las aplicaciones no deben confirmar ni revertir las transacciones mediante la ejecución de instrucciones **commit** o **Rollback** con **SQLExecute** o **SQLExecDirect**. Los efectos de hacerlo son indefinidos. Entre los posibles problemas se incluyen el controlador que ya no sabe cuándo está activa una transacción y que estas instrucciones no superan los orígenes de datos que no admiten transacciones. Estas aplicaciones deben llamar a **SQLEndTran** en su lugar.  
  
 Si una aplicación pasa el identificador de entorno a **SQLEndTran** pero no pasa un identificador de conexión, el administrador de controladores llama conceptualmente a **SQLEndTran** con el identificador de entorno para cada controlador que tenga una o más conexiones activas en el entorno. A continuación, el controlador confirma las transacciones en cada conexión del entorno. Sin embargo, es importante tener en cuentan que ni el controlador ni el administrador de controladores realizan una confirmación en dos fases en las conexiones en el entorno. Esto es simplemente una comodidad de programación para llamar a **SQLEndTran** simultáneamente para todas las conexiones en el entorno.  
  
 (Una *confirmación en dos fases* se utiliza generalmente para confirmar las transacciones que se distribuyen entre varios orígenes de datos. En su primera fase, se sondearán los orígenes de datos para comprobar si pueden confirmar su parte de la transacción. En la segunda fase, la transacción se confirma realmente en todos los orígenes de datos. Si alguno de los orígenes de datos responde en la primera fase en la que no se puede confirmar la transacción, no se produce la segunda fase).
