---
title: Crear una transacción distribuida ? Microsoft Docs
ms.custom: ''
ms.date: 05/13/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- MS DTC, performing distributed transactions
- SQL Server Native Client ODBC driver, transactions
- distributed transactions [ODBC]
- transactions [ODBC]
- ODBC, transactions
ms.assetid: 2c17fba0-7a3c-453c-91b7-f801e7b39ccb
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f21ea9b7146b2907a09688f5189d6d9ae4f3f26a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303714"
---
# <a name="create-a-distributed-transaction"></a>Crear una transacción distribuida

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

<!--
The following includes .md file is Empty, as of long before 2019/May/13.
/includes/snac-deprecated.md
-->


Se puede crear una transacción distribuida para diferentes sistemas Microsoft SQL de diferentes maneras.

## <a name="odbc-driver-calls-the-msdtc-for-sql-server-on-premises"></a>Controlador ODBC llama a MSDTC para SQL Server local

El Coordinador de transacciones distribuidas de Microsoft _distribute_ (MSDTC) permite a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]las aplicaciones extender o distribuir una transacción entre dos o más instancias de . La transacción distribuida funciona incluso cuando las dos instancias se hospedan en equipos independientes.

MSDTC está instalado para Microsoft SQL Server local, pero no está disponible para el servicio en la nube de Azure SQL Database de Microsoft.

MSDTC es llamado por el controlador de SQL ServerSQL Server Native Client para Open Database Connectivity (ODBC), cuando el programa C++ administra una transacción distribuida. El controlador ODBC de Native Client tiene un administrador de transacciones que es compatible con el estándar XA de procesamiento de transacciones distribuidas de grupo abierto (DTP). MSDTC requiere este cumplimiento. Normalmente, todos los comandos de administración de transacciones se envían a través de este controlador ODBC de Native Client. La secuencia es la siguiente:

1. La aplicación ODBC de C++ Native Client inicia una transacción llamando a [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md), con el modo de confirmación automática desactivado.

2. La aplicación actualiza algunos datos en SQL Server X en el equipo A.

3. La aplicación actualiza algunos datos en SQL Server Y en el equipo B.
    - Si se produce un error en una actualización en SQL Server Y, se revierten todas las actualizaciones no confirmadas en ambas instancias de SQL ServerSQL Server .

4. Por último, la aplicación finaliza la transacción llamando a [SQLEndTran _(1)_](../../../relational-databases/native-client-odbc-api/sqlendtran.md), con la opción SQL_COMMIT o SQL_ROLLBACK.

_(1)_ MSDTC se puede invocar sin ODBC. En tal caso, MSDTC se convierte en el administrador de transacciones y la aplicación ya no utiliza **SQLEndTran**.

### <a name="only-one-distributed-transaction"></a>Sólo una transacción distribuida

Supongamos que la aplicación ODBC de C++ Native Client se da de alta en una transacción distribuida. A continuación, la aplicación se da de alta en una segunda transacción distribuida. En este caso, el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC de Native Client deja la transacción distribuida original y se da de alta en la nueva transacción distribuida.

Para obtener más información, consulte [Referencia del programador de DTC](https://docs.microsoft.com/previous-versions/windows/desktop/ms686108\(v=vs.85\)).

## <a name="c-alternative-for-sql-database-in-the-cloud"></a>Alternativa de C- para SQL Database en la nube

MSDTC no es compatible con Azure SQL Database o Azure SQL Data Warehouse.

Sin embargo, se puede crear una transacción distribuida para SQL [System.Transactions.TransactionScope](/dotnet/api/system.transactions.transactionscope)Database mediante el uso del programa de C-

### <a name="other-programming-languages"></a>Otros lenguajes de programación

Es posible que los siguientes lenguajes de programación no proporcionen compatibilidad para transacciones distribuidas con el servicio SQL Database:

- C++ nativo que utilizan controladores ODBC
- Servidor vinculado mediante Transact-SQLTransact-SQL
- Controladores JDBC

## <a name="see-also"></a>Vea también

[Realizar transacciones (ODBC)](performing-transactions-in-odbc.md)
