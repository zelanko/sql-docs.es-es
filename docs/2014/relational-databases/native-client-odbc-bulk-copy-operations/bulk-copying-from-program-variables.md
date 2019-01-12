---
title: Copia masiva desde Variables de programa | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- bulk copy [ODBC], program variables
- bcp_bind function
- mapping data types [ODBC]
- SQL Server Native Client ODBC driver, bulk copy
- data types [ODBC], bulk copying
- ODBC, bulk copy operations
- program variables [ODBC]
ms.assetid: e4284a1b-7534-4b34-8488-b8d05ed67b8c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5473d741f5144338c99627e1057c51ce116093d6
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/09/2019
ms.locfileid: "54130295"
---
# <a name="bulk-copying-from-program-variables"></a>Copia masiva de variables de programa
  Es posible realizar la copia masiva directamente desde variables de programa. Después de asignar variables para almacenar los datos de una fila y llamar a [bcp_init](../native-client-odbc-extensions-bulk-copy-functions/bcp-init.md) para iniciar la copia masiva, llame a [bcp_bind](../native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md) para cada columna especificar la ubicación y el formato de la variable de programa que va a asociar con la columna. Cada variable de relleno con datos, a continuación, llame a [bcp_sendrow](../native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md) para enviar una fila de datos al servidor. Repita el proceso de rellenar las variables y llamar a **bcp_sendrow** hasta que todas las filas se enviaron al servidor, a continuación, llame a [bcp_done](../native-client-odbc-extensions-bulk-copy-functions/bcp-done.md) para especificar que la operación se ha completado.  
  
 El **bcp_bind**_pData_ parámetro contiene la dirección de la variable que se está enlazaba a la columna. Los datos de cada columna pueden almacenarse de una de estas dos formas:  
  
-   Asignando una variable para almacenar los datos.  
  
-   Asignando una variable de indicador inmediatamente seguida de la variable de datos.  
  
 La variable de indicador indica la longitud de los datos para las columnas de longitud variable y también indica los valores NULL, si la columna permite valores NULL. Si solo se usa una variable de datos, la dirección de esta variable se almacena en el **bcp_bind**_pData_ parámetro. Si se usa una variable de indicador, la dirección de la variable de indicador se almacena en el **bcp_bind**_pData_ parámetro. Las funciones de copia masiva calculan la ubicación de la variable de datos agregando el **bcp_bind**_cbIndicator_ y *pData* parámetros.  
  
 **bcp_bind** admite tres métodos para tratar con datos de longitud variable:  
  
-   Uso *cbData* con sólo una variable de datos. Colocar la longitud de los datos de *cbData*. Cada vez que la longitud de los datos de forma masiva copia los cambios, llame a [bcp_collen](../native-client-odbc-extensions-bulk-copy-functions/bcp-collen.md)restablecer *cbData*. Si se está usando uno de los otros dos métodos, especifique SQL_VARLEN_DATA para *cbData*. Si todos los valores de datos que se proporcionan para una columna son NULL, especifique SQL_NULL_DATA para *cbData*.  
  
-   Usar variables de indicador. A medida que cada nuevo valor de datos se pase a la variable de datos, almacene la longitud del valor en la variable de indicador. Si se utiliza uno de los otros dos métodos, especifique 0 para *cbIndicator*.  
  
-   Usar punteros de terminador. Carga el **bcp_bind**_pTerm_ parámetro con la dirección del patrón de bits que finaliza los datos. Si se utiliza uno de los otros dos métodos, especifique NULL para la *pTerm*.  
  
 Tres de estos métodos pueden usarse en el mismo **bcp_bind** llamar, en cuyo caso se usa la especificación que da como resultado la menor cantidad de datos que se va a copiar.  
  
 El **bcp_bind**_tipo_ identificadores de tipo de datos de parámetro usa DB-Library, no ODBC identificadores de tipo de datos. Identificadores de tipo de datos de DB-Library se definen en sqlncli.h para usarse con ODBC **bcp_bind** función.  
  
 Las funciones de copia masiva no admiten todos los tipos de datos C de ODBC. Por ejemplo, las funciones de copia masiva no admiten la estructura SQL_C_TYPE_TIMESTAMP de ODBC, así que use [SQLBindCol](../native-client-odbc-api/sqlbindcol.md) o [SQLGetData](../native-client-odbc-api/sqlgetdata.md) para convertir datos SQL_TYPE_TIMESTAMP de ODBC a una variable SQL_C_CHAR. Si después usa **bcp_bind** con un *tipo* parámetro igual a sqlcharacter para enlazar la variable a un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **datetime** conversión las funciones de copia masiva de columna, el cláusula de escape de marca de tiempo en la variable de caracteres al formato de fecha y hora adecuado.  
  
 En la tabla siguiente se muestran los tipos de datos que es recomendable usar en la asignación de un tipo de datos SQL de ODBC a un tipo de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|Tipo de datos SQL de ODBC|Tipo de datos C de ODBC|bcp_bind *tipo* parámetro|Tipo de datos de SQL Server|  
|-----------------------|----------------------|--------------------------------|--------------------------|  
|SQL_CHAR|SQL_C_CHAR|SQLCHARACTER|**carácter**<br /><br /> **char**|  
|SQL_VARCHAR|SQL_C_CHAR|SQLCHARACTER|**varchar**<br /><br /> **variable de carácter**<br /><br /> **char varying**<br /><br /> **sysname**|  
|SQL_LONGVARCHAR|SQL_C_CHAR|SQLCHARACTER|**texto**|  
|SQL_WCHAR|SQL_C_WCHAR|SQLNCHAR|**nchar**|  
|SQL_WVARCHAR|SQL_C_WCHAR|SQLNVARCHAR|**nvarchar**|  
|SQL_WLONGVARCHAR|SQL_C_WCHAR|SQLNTEXT|**ntext**|  
|SQL_DECIMAL|SQL_C_CHAR|SQLCHARACTER|**decimal**<br /><br /> **dec**<br /><br /> **money**<br /><br /> **smallmoney**|  
|SQL_NUMERIC|SQL_C_NUMERIC|SQLNUMERICN|**numeric**|  
|SQL_BIT|SQL_C_BIT|SQLBIT|**bit**|  
|SQL_TINYINT (con signo)|SQL_C_SSHORT|SQLINT2|**smallint**|  
|SQL_TINYINT (sin signo)|SQL_C_UTINYINT|SQLINT1|**tinyint**|  
|SQL_SMALL_INT (con signo)|SQL_C_SSHORT|SQLINT2|**smallint**|  
|SQL_SMALL_INT (sin signo)|SQL_C_SLONG|SQLINT4|**int**<br /><br /> **integer**|  
|SQL_INTEGER (con signo)|SQL_C_SLONG|SQLINT4|**int**<br /><br /> **integer**|  
|SQL_INTEGER (sin signo)|SQL_C_CHAR|SQLCHARACTER|**decimal**<br /><br /> **dec**|  
|SQL_BIGINT (con signo y sin signo)|SQL_C_CHAR|SQLCHARACTER|**bigint**|  
|SQL_REAL|SQL_C_FLOAT|SQLFLT4|**real**|  
|SQL_FLOAT|SQL_C_DOUBLE|SQLFLT8|**float**|  
|SQL_DOUBLE|SQL_C_DOUBLE|SQLFLT8|**float**|  
|SQL_BINARY|SQL_C_BINARY|SQLBINARY|**binario**<br /><br /> **timestamp**|  
|SQL_VARBINARY|SQL_C_BINARY|SQLBINARY|**varbinary**<br /><br /> **binary varying**|  
|SQL_LONGVARBINARY|SQL_C_BINARY|SQLBINARY|**imagen**|  
|SQL_TYPE_DATE|SQL_C_CHAR|SQLCHARACTER|**datetime**<br /><br /> **smalldatetime**|  
|SQL_TYPE_TIME|SQL_C_CHAR|SQLCHARACTER|**datetime**<br /><br /> **smalldatetime**|  
|SQL_TYPE_TIMESTAMP|SQL_C_CHAR|SQLCHARACTER|**datetime**<br /><br /> **smalldatetime**|  
|SQL_GUID|SQL_C_GUID|SQLUNIQUEID|**uniqueidentifier**|  
|SQL_INTERVAL_|SQL_C_CHAR|SQLCHARACTER|**char**|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no ha firmado **tinyint**sin signo **smallint**, o sin signo **int** tipos de datos. Para impedir la pérdida de valores de datos al migrar estos tipos de datos, cree la tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con el tipo de datos entero inmediatamente superior. Para impedir que los usuarios agreguen después valores que se encuentren fuera del intervalo permitido por el tipo de datos original, aplique una regla a la columna [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para restringir los valores permitidos al intervalo admitido por el tipo de datos de origen inicial:  
  
```  
CREATE TABLE Sample_Ints(STinyIntCol   SMALLINT,  
USmallIntCol INT)  
GO  
CREATE RULE STinyInt_Rule  
AS   
@range >= -128 AND @range <= 127  
GO  
CREATE RULE USmallInt_Rule  
AS   
@range >= 0 AND @range <= 65535  
GO  
sp_bindrule STinyInt_Rule, 'Sample_Ints.STinyIntCol'  
GO  
sp_bindrule USmallInt_Rule, 'Sample_Ints.USmallIntCol'  
GO  
```  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no admite directamente los tipos de datos interval. No obstante, una aplicación puede almacenar secuencias de escape interval como cadenas de caracteres en una columna de caracteres de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . La aplicación puede leerlas para usarlas más tarde, pero no pueden usarse en instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
 Las funciones de copia masiva pueden utilizarse para cargar rápidamente en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] datos leídos de un origen de datos ODBC. Usar [SQLBindCol](../native-client-odbc-api/sqlbindcol.md) para enlazar las columnas de un conjunto de resultados a variables de programa, a continuación, use **bcp_bind** para enlazar las mismas variables de programa a una operación de copia masiva. Una llamada a [SQLFetchScroll](../native-client-odbc-api/sqlfetchscroll.md) o **SQLFetch** , a continuación, se captura una fila de datos del origen de datos ODBC en las variables de programa y llamar al método [bcp_sendrow](../native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md) copias masivas de los datos las variables de programa a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Una aplicación puede utilizar el [bcp_colptr](../native-client-odbc-extensions-bulk-copy-functions/bcp-colptr.md) función siempre que sea necesario cambiar la dirección de la variable de datos originalmente especificada en el **bcp_bind** _pData_ parámetro. Una aplicación puede utilizar el [bcp_collen](../native-client-odbc-extensions-bulk-copy-functions/bcp-collen.md) función siempre que sea necesario para cambiar la longitud de los datos originalmente especificada en el **bcp_bind**_cbData_ parámetro.  
  
 No es posible leer datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en variables de programa utilizando la copia masiva; no existe una función como "bcp_readrow". Solo pueden enviarse datos de la aplicación al servidor.  
  
## <a name="see-also"></a>Vea también  
 [Realizar operaciones de copia masiva &#40;ODBC&#41;](performing-bulk-copy-operations-odbc.md)  
  
  
