---
title: Coordinador de transacciones distribuidas (ODBC)
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- MS DTC, using
ms.assetid: 12a275e1-8c7e-436d-8a4e-b7bee853b35c
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c4c0c042ac0a7236f04261e6750ad7771797a4a9
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: es-ES
ms.lasthandoff: 07/06/2020
ms.locfileid: "86000568"
---
# <a name="use-microsoft-distributed-transaction-coordinator-odbc"></a>Usar Microsoft DTC (Coordinador de transacciones distribuidas) (ODBC)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

    
### <a name="to-update-two-or-more-sql-servers-by-using-ms-dtc"></a>Para actualizar dos o más servidores SQL Server mediante MS DTC  
  
1.  Conéctese a MS DTC utilizando la función OLE DtcGetTransactionManager de MS DTC. Para obtener información acerca de MS DTC, vea Microsoft DTC (Coordinador de transacciones distribuidas).  
  
2.  Llame a SQL DriverConnect una vez para cada conexión SQL Server que desee establecer.  
  
3.  Llame a la función OLE ITransactionDispenser::BeginTransaction de MS DTC para iniciar una transacción MS DTC y obtener un objeto Transaction que represente la transacción.  
  
4.  Llame a [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) una vez o más para cada conexión ODBC que quiera dar de alta en la transacción de MS DTC. Es preciso que el segundo parámetro de [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) sea SQL_ATTR_ENLIST_IN_DTC y que el tercer parámetro sea un objeto Transaction (obtenido en el paso 3).  
  
5.  Llame una vez a [SQLExecDirect](https://go.microsoft.com/fwlink/?LinkId=58399) para cada servidor SQL Server que quiera actualizar.  
  
6.  Llame a la función OLE ITransaction::Commit de MS DTC para confirmar la transacción MS DTC. El objeto Transaction ya no es válido.  

 Para realizar una serie de transacciones MS DTC, repita los pasos del 3 al 6.  
  
 Para liberar la referencia al objeto Transaction, llame a la función OLE ITransaction::Return de MS DTC.  
  
 Para usar una conexión ODBC con una transacción MS DTC y, después, usar la misma conexión con una transacción local de SQL Server, llame a [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) con SQL_DTC_DONE.  
  
> [!NOTE]  
>  También puede llamar a [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) y [SQLExecDirect](https://go.microsoft.com/fwlink/?LinkId=58399) sucesivamente para cada servidor SQL Server en lugar de llamarlos tal y como se sugería anteriormente en los pasos 4 y 5.  
  
## <a name="see-also"></a>Consulte también  
 [Realizar transacciones &#40;&#41;ODBC](https://msdn.microsoft.com/library/f431191a-5762-4f0b-85bb-ac99aff29724)  
  
  
