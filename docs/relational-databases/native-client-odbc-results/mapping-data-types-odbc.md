---
description: Asignar tipos de datos (ODBC)
title: Asignar tipos de datos (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- mapping data types [ODBC]
- result sets [ODBC], data types
- ODBC data types, mapping
- SQL Server Native Client ODBC driver, result sets
- ODBC applications, result sets
- data types [ODBC], mapping
- sql_variant data type
- SQL Server Native Client ODBC driver, data types
ms.assetid: 4ba0924d-9fca-4c48-aced-0a8d817b3dde
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b659380d95adf9149ef22a47544446e1c1349e6b
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97438083"
---
# <a name="mapping-data-types-odbc"></a>Asignar tipos de datos (ODBC)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client asigna [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de datos SQL a tipos de datos SQL de ODBC. En las secciones siguientes se describen los tipos de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL y los tipos de datos ODBC SQL a los que se asignan. También se tratan los tipos de datos ODBC SQL y sus tipos de datos ODBC C correspondientes, así como las conversiones compatibles y predeterminadas.  
  
> [!NOTE]  
>  El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de datos **timestamp** se asigna al tipo de datos SQL_BINARY o SQL_VARBINARY ODBC porque los valores de las columnas **timestamp** no son valores **DateTime** , sino valores **binarios (8)** o **varbinary (8)** que indican la secuencia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] actividad de la fila. Si el controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client encuentra un valor SQL_C_WCHAR (Unicode) con un número impar de bytes, se trunca el byte impar final.  
  
## <a name="dealing-with-sql_variant-data-type-in-odbc"></a>Administrar tipos de datos sql_variant en ODBC  
 La columna tipo de datos **sql_variant** puede contener cualquiera de los tipos de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , excepto los objetos grandes (LOB), como **Text**, **ntext** e **Image**. Por ejemplo, la columna puede contener valores **smallint** para algunas filas, valores **float** para otras filas y valores **CHAR/NCHAR** en el resto.  
  
 El tipo de datos **sql_variant** es similar al tipo de datos **variant** de Microsoft Visual Basic®.  
  
### <a name="retrieving-data-from-the-server"></a>Recuperar datos del servidor  
 ODBC no tiene un concepto de tipos Variant, lo que limita el uso del tipo de datos **sql_variant** con un controlador ODBC en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , si se especifica Binding, el tipo de datos **sql_variant** debe estar enlazado a uno de los tipos de datos ODBC documentados. **SQL_CA_SS_VARIANT_TYPE**, un nuevo atributo específico del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client, devuelve el tipo de datos de una instancia de la columna **sql_variant** al usuario.  
  
 Si no se especifica ningún enlace, la función [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md) se puede utilizar para determinar el tipo de datos de una instancia en la columna **sql_variant** .  
  
 Para recuperar los datos de **sql_variant** siga estos pasos.  
  
1.  Llame a **SQLFetch** para colocar en la fila recuperada.  
  
2.  Llame a **SQLGetData**, especificando SQL_C_BINARY para el tipo y 0 para la longitud de los datos. Esto obliga al controlador a leer el encabezado **sql_variant** . El encabezado proporciona el tipo de datos de esa instancia en el **sql_variant** columna. **SQLGetData** devuelve el tamaño (en bytes) del valor.  
  
3.  Llame a [SQLColAttribute](../../relational-databases/native-client-odbc-api/sqlcolattribute.md) especificando **SQL_CA_SS_VARIANT_TYPE** como su valor de atributo. Esta función devolverá el tipo de datos C de la instancia de de la columna **sql_variant** al cliente.  
  
 A continuación se incluye un segmento de código que muestra los pasos anteriores.  
  
```  
while ((retcode = SQLFetch (hstmt))==SQL_SUCCESS)  
{  
    if (retcode != SQL_SUCCESS && retcode != SQL_SUCCESS_WITH_INFO)  
    {  
        SQLError (NULL, NULL, hstmt, NULL,   
                    &lNativeError,szError,MAX_DATA,&sReturned);  
        printf_s ("%s\n",szError);  
        goto Exit;  
    }  
    retcode = SQLGetData (hstmt, 1, SQL_C_BINARY,   
                                pBuff,0,&Indicator);//Figure out the length  
    if (retcode != SQL_SUCCESS_WITH_INFO && retcode != SQL_SUCCESS)  
    {  
        SQLError (NULL, NULL, hstmt, NULL, &lNativeError,   
                    szError,MAX_DATA,&sReturned);  
        printf_s ("%s\n",szError);  
        goto Exit;  
    }  
    printf_s ("Byte length : %d ",Indicator); //Print out the byte length  
  
    int iValue = 0;  
    retcode = SQLColAttribute (hstmt, 1, SQL_CA_SS_VARIANT_TYPE, NULL,   
                                        NULL,NULL,&iValue);  //Figure out the type  
    printf_s ("Sub type = %d ",iValue);//Print the type, the return is C_type of the column]  
  
// Set up a new binding or do the SQLGetData on that column with   
// the appropriate type  
}  
```  
  
 Si el usuario crea el enlace mediante [SQLBindCol](../../relational-databases/native-client-odbc-api/sqlbindcol.md), el controlador Lee los metadatos y los datos. A continuación, el controlador convierte los datos al tipo ODBC adecuado especificado en el enlace.  
  
### <a name="sending-data-to-the-server"></a>Enviar datos al servidor  
 **SQL_SS_VARIANT**, se utiliza un nuevo tipo de datos específico del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client para los datos enviados a una columna **sql_variant** . Al enviar datos al servidor mediante parámetros (por ejemplo, INSERT INTO TableName VALUEs (?,?)), [SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md) se usa para especificar la información de parámetros, incluido el tipo C y el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo correspondiente. El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client convertirá el tipo de datos C en uno de los subtipos **sql_variant** adecuados.  
  
## <a name="see-also"></a>Consulte también  
 [Procesar los resultados &#40;ODBC&#41;](../../relational-databases/native-client-odbc-results/processing-results-odbc.md)  
  
  
