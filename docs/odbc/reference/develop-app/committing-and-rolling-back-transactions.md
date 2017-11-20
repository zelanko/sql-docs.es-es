---
title: Confirmar y revertir las transacciones | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- rolling back transactions [ODBC]
- committing transactions [ODBC]
- transactions [ODBC], rolling back
- transactions [ODBC], committing
ms.assetid: 800f2c1a-6f79-4ed1-830b-aa1a62ff5165
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4090e609063b74fdcbef694c400272ee6af090c5
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="committing-and-rolling-back-transactions"></a>Confirmar y revertir las transacciones
Para confirmar o revertir una transacción en modo de confirmación manual, una aplicación llama **SQLEndTran**. Controladores para DBMS que admiten transacciones normalmente implementan esta función mediante la ejecución de un **confirmar** o **reversión** instrucción. El Administrador de controladores no llama a **SQLEndTran** cuando la conexión está en modo de confirmación automática; simplemente devuelve SQL_SUCCESS, incluso si la aplicación intenta revertir la transacción. Puesto que los controladores para DBMS que no admiten transacciones siempre están en modo de confirmación automática, pueden cualquier implemente **SQLEndTran** para devolver SQL_SUCCESS sin hacer nada o no implementarla.  
  
> [!NOTE]  
>  Las aplicaciones no deben confirmar o revertir las transacciones mediante la ejecución de **confirmación** o **reversión** instrucciones con **SQLExecute** o **SQLExecDirect**. Los efectos de realizar esta tarea no están definidos. Los problemas posibles incluyen el controlador ya no saber cuándo una transacción está activa y estas instrucciones producen errores en los orígenes de datos que no se admiten transacciones. Deben llamar estas aplicaciones **SQLEndTran** en su lugar.  
  
 Si una aplicación pasa el identificador de entorno a **SQLEndTran** pero no no pase un identificador de conexión, el Administrador de controladores conceptualmente llama **SQLEndTran** con el identificador de entorno para cada controlador que tiene una o más conexiones activas en el entorno. El controlador, a continuación, confirma las transacciones en cada conexión en el entorno. Sin embargo, es importante tener en cuenta que el controlador ni el Administrador de controladores realiza una confirmación en dos fases en las conexiones en el entorno; Esto es simplemente una comodidad en la programación para llamar simultáneamente a **SQLEndTran** para todas las conexiones en el entorno.  
  
 (Un *confirmación en dos fases* generalmente se utiliza para confirmar las transacciones que están repartidas en varios orígenes de datos. En su primera fase, se sondean los orígenes de datos en cuanto a si puede confirmar su parte de la transacción. En la segunda fase, la transacción se confirma realmente en todos los orígenes de datos. Si los orígenes de datos de respuesta en la primera fase que cuando no pueden confirmar la transacción, la segunda fase no se produce.)

