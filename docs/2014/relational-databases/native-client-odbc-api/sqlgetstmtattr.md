---
title: SQLGetStmtAttr | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLGetStmtAttr function
ms.assetid: e64f4f94-eb73-4477-9745-080b6cbdc751
caps.latest.revision: 43
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 5c6f1220685b2e9f72df52ddea9c1f676453b856
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36201370"
---
# <a name="sqlgetstmtattr"></a>SQLGetStmtAttr
  El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC Native Client extiende SQLGetStmtAttr para exponer atributos de instrucción específicos del controlador.  
  
 [SQLSetStmtAttr](sqlsetstmtattr.md) listas de los atributos de instrucción tanto de lectura y escritura. En este tema se enumeran los atributos de instrucción de solo lectura.  
  
## <a name="sqlsoptsscurrentcommand"></a>SQL_SOPT_SS_CURRENT_COMMAND  
 El atributo SQL_SOPT_SS_CURRENT_COMMAND expone el comando actual de un lote de comandos. El retorno es un entero que especifica la ubicación del comando en el lote. El valor de *ValuePtr* es de tipo SQLLEN.  
  
## <a name="sqlsoptssnocountstatus"></a>SQL_SOPT_SS_NOCOUNT_STATUS  
 El atributo SQL_SOPT_SS_NOCOUNT_STATUS indica la configuración actual de la NOCOUNT opción, que controla si [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] notifica los números de filas afectadas por una instrucción cuando [SQLRowCount](sqlrowcount.md) se llama. El valor de *ValuePtr* es de tipo SQLLEN.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|SQL_NC_OFF|NOCOUNT es OFF. SQLRowCount devuelve el número de filas afectadas.|  
|SQL_NC_ON|NOCOUNT es ON. No se devuelve el número de filas afectadas por SQLRowCount y el valor devuelto es 0.|  
  
 Si SQLRowCount devuelve 0, la aplicación debe probar SQL_SOPT_SS_NOCOUNT_STATUS. Si se devuelve SQL_NC_ON, el valor de 0 en SQLRowCount sólo indica que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no ha devuelto un recuento de filas. Si devuelve sql_nc_off, significa que NOCOUNT está desactivado y el valor de 0 en SQLRowCount indica que la instrucción no afectó a ninguna fila.  
  
 Las aplicaciones no deben mostrar el valor de SQLRowCount cuando SQL_SOPT_SS_NOCOUNT_STATUS es SQL_NC_OFF. Los lotes o los procedimientos almacenados grandes pueden contener varias instrucciones SET NOCOUNT, así que no se puede asumir que SQL_SOPT_SS_NOCOUNT_STATUS permanezca constante. Esta opción debe probarse cada vez que SQLRowCount devuelve 0.  
  
## <a name="sqlsoptssquerynotificationmsgtext"></a>SQL_SOPT_SS_QUERYNOTIFICATION_MSGTEXT  
 El atributo SQL_SOPT_SS_QUERYNOTIFICATION_MSGTEXT devuelve el texto del mensaje de la solicitud de notificación de consulta.  
  
## <a name="sqlgetstmtattr-and-table-valued-parameters"></a>SQLGetStmtAttr y los parámetros de valores de tabla  
 SQLGetStmtAttr se puede llamar para obtener el valor de SQL_SOPT_SS_PARAM_FOCUS en el descriptor de parámetro de la aplicación (APD) cuando se trabaja con parámetros con valores de tabla. Para obtener más información sobre SQL_SOPT_SS_PARAM_FOCUS, vea [SQLSetStmtAttr](sqlsetstmtattr.md).  
  
 Para obtener más información acerca de los parámetros con valores de tabla, vea [parámetros con valores de tabla &#40;ODBC&#41;](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="see-also"></a>Vea también  
 [SQLSetStmtAttr, función](http://go.microsoft.com/fwlink/?LinkId=59370)   
 [Detalles de implementación de la API de ODBC](odbc-api-implementation-details.md)  
  
  