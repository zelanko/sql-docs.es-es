---
title: SQLGetStmtAttr ? Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLGetStmtAttr function
ms.assetid: e64f4f94-eb73-4477-9745-080b6cbdc751
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f59b7f006387beea3d213b7f120e567487232e69
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282103"
---
# <a name="sqlgetstmtattr"></a>SQLGetStmtAttr
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client extiende SQLGetStmtAttr para exponer atributos de instrucción específicos del controlador.  
  
 [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) enumera los atributos de instrucción de lectura y escritura. En este tema se enumeran los atributos de instrucción de solo lectura.  
  
## <a name="sql_sopt_ss_current_command"></a>SQL_SOPT_SS_CURRENT_COMMAND  
 El atributo SQL_SOPT_SS_CURRENT_COMMAND expone el comando actual de un lote de comandos. El retorno es un entero que especifica la ubicación del comando en el lote. El valor de *ValuePtr* es de tipo SQLLEN.  
  
## <a name="sql_sopt_ss_nocount_status"></a>SQL_SOPT_SS_NOCOUNT_STATUS  
 El atributo SQL_SOPT_SS_NOCOUNT_STATUS indica el valor actual de la opción NOCOUNT, que controla si [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] notifica los números de filas afectados por una instrucción cuando se llama a [SQLRowCount](../../relational-databases/native-client-odbc-api/sqlrowcount.md) . El valor de *ValuePtr* es de tipo SQLLEN.  
  
|Value|Descripción|  
|-----------|-----------------|  
|SQL_NC_OFF|NOCOUNT es OFF. SQLRowCount devuelve el número de filas afectadas.|  
|SQL_NC_ON|NOCOUNT es ON. SQLRowCount no devuelve el número de filas afectadas y el valor devuelto es 0.|  
  
 Si SQLRowCount devuelve 0, la aplicación debe probar SQL_SOPT_SS_NOCOUNT_STATUS. Si se devuelve SQL_NC_ON, el valor de 0 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de SQLRowCount solo indica que no ha devuelto un recuento de filas. Si devuelve SQL_NC_OFF, significa que NOCOUNT está desactivado y el valor de 0 en SQLRowCount indica que la instrucción no afectó a ninguna fila.  
  
 Las aplicaciones no deben mostrar el valor de SQLRowCount cuando SQL_SOPT_SS_NOCOUNT_STATUS es SQL_NC_OFF. Los lotes o los procedimientos almacenados grandes pueden contener varias instrucciones SET NOCOUNT, así que no se puede asumir que SQL_SOPT_SS_NOCOUNT_STATUS permanezca constante. Esta opción se debe probar cada vez que SQLRowCount devuelve 0.  
  
## <a name="sql_sopt_ss_querynotification_msgtext"></a>SQL_SOPT_SS_QUERYNOTIFICATION_MSGTEXT  
 El atributo SQL_SOPT_SS_QUERYNOTIFICATION_MSGTEXT devuelve el texto del mensaje de la solicitud de notificación de consulta.  
  
## <a name="sqlgetstmtattr-and-table-valued-parameters"></a>SQLGetStmtAttr y los parámetros de valores de tabla  
 SQLGetStmtAttr se puede llamar para obtener el valor de SQL_SOPT_SS_PARAM_FOCUS en el descriptor de parámetro de aplicación (APD) al trabajar con parámetros con valores de tabla. Para obtener más información sobre SQL_SOPT_SS_PARAM_FOCUS, vea [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md).  
  
 Para obtener más información acerca de los parámetros con valores de tabla, vea [Parámetros con valores ](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)de tabla &#40;&#41;ODBC .  
  
## <a name="see-also"></a>Consulte también  
 [Función SQLSetStmtAttr](https://go.microsoft.com/fwlink/?LinkId=59370)   
 [ODBC API Implementation Details](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
