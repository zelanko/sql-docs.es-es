---
title: Confirmar y revertir las transacciones | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 194a90482946814995ca1963f7c8fc4bce48d223
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63126368"
---
# <a name="committing-and-rolling-back-transactions"></a>Confirmar y revertir las transacciones
Para confirmar o revertir una transacción en modo de confirmación manual, una aplicación llama a **SQLEndTran**. Controladores para DBMS que admiten transacciones suelen implementan esta función mediante la ejecución de un **confirmar** o **reversión** instrucción. El Administrador de controladores no llama a **SQLEndTran** cuando la conexión está en modo de confirmación automática; simplemente devuelve SQL_SUCCESS, incluso si la aplicación intenta revertir la transacción. Dado que los controladores para DBMS que no admiten transacciones siempre están en modo de confirmación automática, puede implementar **SQLEndTran** para devolver SQL_SUCCESS sin hacer nada o no implementarlo.  
  
> [!NOTE]  
>  Las aplicaciones no deben confirmar o revertir las transacciones mediante la ejecución de **confirmación** o **reversión** instrucciones con **SQLExecute** o **SQLExecDirect**. Los efectos de realizar esta tarea son indefinidos. Posibles problemas incluyen el controlador ya no saber cuando una transacción está activa y estas instrucciones producen errores en los orígenes de datos que no admiten transacciones. Estas aplicaciones deberían llamar a **SQLEndTran** en su lugar.  
  
 Si una aplicación pasa el identificador de entorno **SQLEndTran** pero no pase un identificador de conexión, el Administrador de controladores conceptualmente llama **SQLEndTran** con el identificador del entorno para cada controlador que tiene uno o más conexiones activas en el entorno. El controlador, a continuación, confirma las transacciones en cada conexión en el entorno. Sin embargo, es importante tener en cuenta que el controlador ni el Administrador de controladores realiza una confirmación en dos fases en las conexiones en el entorno; Esto es simplemente una comodidad en la programación para llamar simultáneamente a **SQLEndTran** para todas las conexiones en el entorno.  
  
 (Un *confirmación en dos fases* generalmente se usa para confirmar las transacciones que están repartidas entre varios orígenes de datos. En su primera fase, se sondean los orígenes de datos que se pueden confirmar si su parte de la transacción. En la segunda fase, la transacción se confirma realmente en todos los orígenes de datos. Si los orígenes de datos de respuesta en la primera fase que no pueden confirmar la transacción, la segunda fase no se produce.)
