---
title: Transacciones en ODBC | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, transactions
- transactions [ODBC]
- ODBC, transactions
ms.assetid: c5a87fa5-827a-4e6f-a0d9-924bac881eb0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ade18b71fa83c7acbb16cb7facd19dd3de61a2e3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "63143324"
---
# <a name="transactions-in-odbc"></a>Transacciones en ODBC
  Las transacciones en ODBC se administran en las conexiones. Cuando una aplicación completa una transacción, confirma o revierte todo el trabajo completado a través de todos los identificadores de instrucciones de dicha conexión. Para confirmar o revertir una transacción, las aplicaciones deberían llamar a [SQLEndTran](../../native-client-odbc-api/sqlendtran.md) en lugar de enviar una instrucción COMMIT o ROLLBACK.  
  
 Una aplicación llama a [SQLSetConnectAttr](../../native-client-odbc-api/sqlsetconnectattr.md) para intercambiar entre los dos modos ODBC de administrar transacciones:  
  
-   Modo de confirmación automática  
  
     Todas las instrucciones se confirman automáticamente cuando se completan correctamente. Cuando se ejecuta en modo de confirmación automática, no se requiere ninguna otra función de administración de transacciones.  
  
-   Modo de confirmación manual  
  
     Todos las instrucciones ejecutadas se incluyen en la misma transacción hasta que se detenga específicamente llamando a **SQLEndTran**.  
  
 El modo de confirmación automática es el modo de transacción para ODBC. Cuando se realiza una conexión, se encuentra en modo de confirmación automática hasta que se llame a **SQLSetConnectAttr** para pasar al modo de confirmación manual desactivando el modo de confirmación automática. Cuando una aplicación desactiva la confirmación automática, la siguiente instrucción enviada a la base de datos inicia una transacción. A continuación, la transacción permanece activa hasta que la aplicación llama a **SQLEndTran** con las opciones SQL_COMMIT o SQL_ROLLBACK. El comando enviado a la base de datos después de que **SQLEndTran** inicia la siguiente transacción.  
  
 Si una aplicación pasa del modo de confirmación manual al modo de confirmación automática, el controlador confirma cualquier transacción actualmente abierta en la conexión.  
  
 Las aplicaciones ODBC no deberían usar instrucciones de transacción de Transact-SQL como BEGIN TRANSACTION, COMMIT TRANSACTION o ROLLBACK TRANSACTION porque esto puede producir un comportamiento indeterminado en el controlador. Una aplicación ODBC se debería ejecutar en modo de confirmación automática y no usar instrucciones o funciones de administración de transacciones o bien, ejecutarse en el modo de confirmación manual y usar la función **SQLEndTran** ODBC para confirmar o revertir transacciones.  
  
## <a name="see-also"></a>Consulte también  
 [Realizar transacciones &#40;&#41;ODBC](../../../database-engine/dev-guide/performing-transactions-odbc.md)  
  
  
