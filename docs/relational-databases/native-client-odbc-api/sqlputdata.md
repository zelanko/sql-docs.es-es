---
title: SQLPutData | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLPutData function
ms.assetid: d39aaa5b-7fbc-4315-a7f2-5a7787e04f25
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8a9648fac10c5bc6d5e893bad123bbe02c38bc29
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: es-ES
ms.lasthandoff: 07/06/2020
ms.locfileid: "86009899"
---
# <a name="sqlputdata"></a>SQLPutData
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Se aplican las siguientes restricciones al usar SQLPutData para enviar más de 65.535 bytes de datos (para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] la versión 4.21 a) o 400 KB de datos (para SQL Server versión 6,0 y posteriores) para una columna SQL_LONGVARCHAR (**texto**), SQL_WLONGVARCHAR (**ntext**) o SQL_LONGVARBINARY (**imagen**):  
  
-   El parámetro al que se hace referencia puede ser el *insert_value* en una instrucción INSERT.  
  
-   El parámetro al que se hace referencia puede ser una *expresión* de la cláusula SET de una instrucción UPDATE.  
  
 Al cancelar una secuencia de llamadas a SQLPutData que proporcionan datos en bloques a un servidor que ejecuta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , se produce una actualización parcial del valor de la columna cuando se usa la versión 6,5 o anterior. La columna **Text**, **ntext**o **Image** a la que se hizo referencia cuando se llamó a SQLCancel se establece en un valor de marcador de posición intermedio.  
  
> [!NOTE]  
>  El controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client no permite la conexión con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versión 6.5 y anteriores.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Hay un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQLSTATE específico del cliente nativo para SQLPutData:  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|22026|Datos de cadena, desigualdad de longitud|Si una aplicación ha especificado la longitud de los datos en bytes que se van a enviar, por ejemplo, con SQL_LEN_DATA_AT_EXEC (*n*), donde *n* es mayor que 0, el número total de bytes proporcionado por la aplicación a través de SQLPutData debe coincidir con la longitud especificada.|  
  
## <a name="sqlputdata-and-table-valued-parameters"></a>SQLPutData y parámetros con valores de tabla  
 Una aplicación utiliza SQLPutData cuando se usa el enlace de filas variable con parámetros con valores de tabla. El parámetro *StrLen_Or_Ind* indica que está listo para que el controlador recopile datos de la siguiente fila o filas de datos de parámetros con valores de tabla, o que no haya más filas disponibles:  
  
-   Un valor mayor que 0 indica que el conjunto siguiente de valores de fila está disponible.  
  
-   Un valor de 0 indica que no hay ninguna fila más para enviar.  
  
-   Cualquier valor menor que 0 es un error tiene como resultado un registro de diagnóstico que se registra con con SQLState HY090 y el mensaje "Longitud de búfer o cadena no válida".  
  
 Se omite el parámetro *DataPtr* , pero debe establecerse en un valor distinto de NULL. Para obtener más información, vea la sección sobre el enlace de filas variable TVP en [Binding y transferencia de datos de parámetros con valores de tabla y valores de columna](../../relational-databases/native-client-odbc-table-valued-parameters/binding-and-data-transfer-of-table-valued-parameters-and-column-values.md).  
  
 Si *StrLen_Or_Ind* tiene un valor distinto de SQL_DEFAULT_PARAM o un número entre 0 y el SQL_PARAMSET_SIZE (es decir, el parámetro *columnas* de SQLBindParameter), se trata de un error. Este error hace que SQLPutData devuelva SQL_ERROR: SQLSTATE=HY090, "Longitud de búfer o cadena no válida".  
  
 Para obtener más información sobre los parámetros con valores de tabla, vea [parámetros con valores de tabla &#40;ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="sqlputdata-support-for-enhanced-date-and-time-features"></a>Compatibilidad de SQLPutData con las características mejoradas de fecha y hora  
 Los valores de parámetro de los tipos de fecha y hora se convierten como se describe en [conversiones de C a SQL](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-from-c-to-sql.md).  
  
 Para obtener más información, vea [mejoras de fecha y hora &#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlputdata-support-for-large-clr-udts"></a>Compatibilidad de SQLPutData con los UDT CLR grandes  
 **SQLPutData** admite tipos definidos por el usuario (UDT) CLR grandes. Para obtener más información, vea [tipos CLR grandes definidos por el usuario &#40;ODBC&#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Consulte también  
 [SQLPutData función)](https://go.microsoft.com/fwlink/?LinkId=59365)   
 [ODBC API Implementation Details](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
