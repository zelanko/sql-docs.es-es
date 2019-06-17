---
title: Crear un transacciones distribuidas | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8ea6c4886a3c5397777b7a65afe96ab7e1b422bd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65620544"
---
# <a name="create-a-distributed-transaction"></a>Crear una transacción distribuida

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

<!--
The following includes .md file is Empty, as of long before 2019/May/13.
/includes/snac-deprecated.md
-->

[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

Una transacción distribuida se puede crear para los distintos sistemas de Microsoft SQL de maneras diferentes.

## <a name="odbc-driver-calls-the-msdtc-for-sql-server-on-premises"></a>Controlador ODBC llama a MSDTC para SQL Server local

El Coordinador de transacciones distribuidas de Microsoft (MSDTC) permite a las aplicaciones ampliar o _distribuir_ una transacción entre dos o más instancias de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. La transacción distribuida funciona incluso cuando las dos instancias se hospedan en equipos independientes.

MSDTC está instalado para Microsoft SQL Server local, pero no está disponible para el servicio de nube de Microsoft Azure SQL Database.

MSDTC es llamado por el controlador de SQL Server Native Client para conectividad abierta de base de datos (ODBC), cuando su C++ programa administra una transacción distribuida. El controlador ODBC de Native Client tiene un administrador de transacciones que sea compatible con el Abrir grupo Distributed transacción procesamiento (DTP) estándar XA. Se requiere este cumplimiento por MSDTC. Por lo general, todos los comandos de administración de transacciones se envían a través de este controlador ODBC de Native Client. La secuencia es como sigue:

1. Su C++ aplicación ODBC de Native Client comienza una transacción mediante una llamada a [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md), con el modo de confirmación automática desactivado.

2. La aplicación actualiza algunos datos en SQL Server X en el equipo A.

3. La aplicación actualiza algunos datos en SQL Server Y en el equipo B.
    - Si una actualización en SQL Server Y se produce un error, se revierten todas las actualizaciones no confirmadas en ambas instancias de SQL Server.

4. Por último, la la aplicación finaliza la transacción mediante una llamada [SQLEndTran _(1)_ ](../../../relational-databases/native-client-odbc-api/sqlendtran.md), con las opciones SQL_COMMIT o SQL_ROLLBACK.

_(1)_  MSDTC puede invocarse sin ODBC. En tal caso, MSDTC, se convierte en el Administrador de transacciones y la aplicación ya no utiliza **SQLEndTran**.

### <a name="only-one-distributed-transaction"></a>Solo una transacción distribuida

Suponga que su C++ aplicación ODBC de Native Client se da de alta en una transacción distribuida. A continuación la aplicación da de alta en una segunda transacción distribuida. En este caso, el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC de Native Client deja la transacción distribuida original y se inscribe en la nueva transacción distribuida.

Para obtener más información, consulte [referencia del programador de DTC](https://docs.microsoft.com/previous-versions/windows/desktop/ms686108\(v=vs.85\)).

## <a name="c-alternative-for-sql-database-in-the-cloud"></a>C#alternativa para la base de datos de SQL en la nube

MSDTC no se admite para Azure SQL Database o Azure SQL Data Warehouse.

Sin embargo, se puede crear una transacción distribuida para la base de datos SQL al tener su C# programa utilice la clase de .NET [System.Transactions.TransactionScope](/dotnet/api/system.transactions.transactionscope).

### <a name="other-programming-languages"></a>Otros lenguajes de programación

La siguiente es posible que otros lenguajes de programación no ofrece ninguna compatibilidad para las transacciones distribuidas con el servicio de base de datos de SQL:

- Nativo C++ que usan los controladores ODBC
- Servidor vinculado mediante Transact-SQL
- Controladores JDBC

## <a name="see-also"></a>Vea también

[Realizar transacciones (ODBC)](performing-transactions-in-odbc.md)
