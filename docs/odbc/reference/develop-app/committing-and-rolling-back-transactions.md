---
title: Comprometiendo y revirtiendo transacciones ? Microsoft Docs
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
ms.openlocfilehash: 1c272d60242d31622452c4dcb0f6a16c4838768f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299115"
---
# <a name="committing-and-rolling-back-transactions"></a>Confirmar y revertir las transacciones
Para confirmar o revertir una transacción en modo de confirmación manual, una aplicación llama a **SQLEndTran**. Los controladores para DBMS que admiten transacciones normalmente implementan esta función mediante la ejecución de una instrucción **COMMIT** o **ROLLBACK.** El Administrador de controladores no llama a **SQLEndTran** cuando la conexión está en modo de confirmación automática; simplemente devuelve SQL_SUCCESS, incluso si la aplicación intenta revertir la transacción. Dado que los controladores para DBMS que no admiten transacciones siempre están en modo de confirmación automática, pueden implementar **SQLEndTran** para devolver SQL_SUCCESS sin hacer nada o no implementarlo en absoluto.  
  
> [!NOTE]  
>  Las aplicaciones no deben confirmar ni revertir transacciones ejecutando instrucciones **COMMIT** o **ROLLBACK** con **SQLExecute** o **SQLExecDirect**. Los efectos de hacer esto son indefinidos. Entre los posibles problemas se incluyen que el controlador ya no sabe cuándo está activa una transacción y que estas instrucciones fallan en orígenes de datos que no admiten transacciones. Estas aplicaciones deben llamar a **SQLEndTran** en su lugar.  
  
 Si una aplicación pasa el identificador de entorno a **SQLEndTran** pero no pasa un identificador de conexión, el Administrador de controladores llama conceptualmente **SQLEndTran** con el identificador de entorno para cada controlador que tiene una o más conexiones activas en el entorno. A continuación, el controlador confirma las transacciones en cada conexión del entorno. Sin embargo, es importante tener en cuenta que ni el controlador ni el Administrador de controladores realizan una confirmación de dos fases en las conexiones en el entorno; esto es simplemente una conveniencia de programación para llamar simultáneamente a **SQLEndTran** para todas las conexiones en el entorno.  
  
 (Una *confirmación de dos fases* se utiliza generalmente para confirmar transacciones que se distribuyen entre varios orígenes de datos. En su primera fase, se sondean los orígenes de datos en cuanto a si pueden confirmar su parte de la transacción. En la segunda fase, la transacción se confirma realmente en todos los orígenes de datos. Si algún origen de datos responde en la primera fase que no puede confirmar la transacción, la segunda fase no se produce.)
