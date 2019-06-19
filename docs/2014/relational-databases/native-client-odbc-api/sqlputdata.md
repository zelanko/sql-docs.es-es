---
title: SQLPutData | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLPutData function
ms.assetid: d39aaa5b-7fbc-4315-a7f2-5a7787e04f25
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7e15353cd9f4c4a837fe5978d00259ad5460d50d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63046630"
---
# <a name="sqlputdata"></a>SQLPutData
  Las restricciones siguientes se aplican al usar SQLPutData para enviar más de 65.535 bytes de datos (para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versión 4. 21a) o 400 KB de datos (para SQL Server versión 6.0 y versiones posterior) para un SQL_LONGVARCHAR (`text`), SQL_WLONGVARCHAR (`ntext`) o SQL_LONGVARBINARY (`image`) columna:  
  
-   El parámetro que se hace referencia puede ser el *insert_value* en una instrucción INSERT.  
  
-   El parámetro que se hace referencia puede ser un *expresión* en la cláusula SET de una instrucción UPDATE.  
  
 Cancelación de una secuencia de llamadas de SQLPutData que proporcionan datos en bloques a un servidor que ejecuta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hace que una actualización parcial del valor de la columna cuando se usa la versión 6.5 o anterior. El `text`, `ntext`, o `image` columna que se hizo referencia cuando se llamó a SQLCancel está establecida en un valor de marcador de posición intermedio.  
  
> [!NOTE]  
>  El controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client no permite la conexión con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versión 6.5 y anteriores.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Hay un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQLSTATE específico de cliente nativo de SQLPutData:  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|22026|Datos de cadena, desigualdad de longitud|Si la longitud de datos en bytes que se enviarán se ha especificado por una aplicación, por ejemplo, con SQL_LEN_DATA_AT_EXEC (*n*) donde *n* es mayor que 0, el número total de bytes proporcionado por la aplicación a través de SQLPutData debe coincidir con la longitud especificada.|  
  
## <a name="sqlputdata-and-table-valued-parameters"></a>SQLPutData y parámetros con valores de tabla  
 SQLPutData está usando una aplicación cuando se usa el enlace de filas variable con parámetros con valores de tabla. El *StrLen_Or_Ind* parámetro indica que está listo para el controlador recopilar datos de la siguiente fila o filas de datos del parámetro con valores de tabla, o que no hay más filas disponibles:  
  
-   Un valor mayor que 0 indica que el conjunto siguiente de valores de fila está disponible.  
  
-   Un valor de 0 indica que no hay ninguna fila más para enviar.  
  
-   Cualquier valor menor que 0 es un error tiene como resultado un registro de diagnóstico que se registra con con SQLState HY090 y el mensaje "Longitud de búfer o cadena no válida".  
  
 El *DataPtr* parámetro se omite, pero debe establecerse en un valor distinto de NULL. Para obtener más información, vea la sección sobre el enlace de filas Variable TVP en [enlace y Data Transfer of Table-Valued parámetros y valores de columna](../native-client-odbc-table-valued-parameters/binding-and-data-transfer-of-table-valued-parameters-and-column-values.md).  
  
 Si *StrLen_Or_Ind* tiene cualquier valor distinto de SQL_DEFAULT_PARAM o un número entre 0 y el parámetro SQL_PARAMSET_SIZE (es decir, el *ColumnSize* parámetro de SQLBindParameter), es un error. Este error hace que SQLPutData devuelva SQL_ERROR: SQLSTATE = HY090, "Longitud de búfer o cadena no válida".  
  
 Para obtener más información acerca de los parámetros con valores de tabla, vea [parámetros con valores de tabla &#40;ODBC&#41;](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="sqlputdata-support-for-enhanced-date-and-time-features"></a>Compatibilidad de SQLPutData con las características mejoradas de fecha y hora  
 Los valores de parámetro de tipos de fecha y hora se convierten como se describe en [conversiones de C a SQL](../native-client-odbc-date-time/datetime-data-type-conversions-from-c-to-sql.md).  
  
 Para obtener más información, consulte [mejoras de fecha y hora &#40;ODBC&#41;](../native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlputdata-support-for-large-clr-udts"></a>Compatibilidad de SQLPutData con los UDT CLR grandes  
 `SQLPutData` admite tipos CLR definidos por el usuario (UDT) grandes. Para obtener más información, consulte [Large CLR User-Defined tipos &#40;ODBC&#41;](../native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Vea también  
 [Función SQLPutData](https://go.microsoft.com/fwlink/?LinkId=59365)   
 [Detalles de implementación de la API de ODBC](odbc-api-implementation-details.md)  
  
  
