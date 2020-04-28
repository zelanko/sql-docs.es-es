---
title: bcp_bind | Microsoft Docs
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.technology: native-client
ms.topic: reference
apiname:
- bcp_bind
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_bind function
ms.assetid: 6e335a5c-64b2-4bcf-a88f-35dc9393f329
author: markingmyname
ms.author: maghan
ms.custom: ''
ms.reviewer: ''
ms.date: 03/14/2017
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 601a584a315eba7013c086dc59c9fb5bfeff8693
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "73783219"
---
# <a name="bcp_bind"></a>bcp_bind

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Enlaza los datos de una variable de programa a una columna de tabla para la copia masiva en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  

## <a name="syntax"></a>Sintaxis

```  
  
RETCODE bcp_bind (  
        HDBC hdbc,
        LPCBYTE pData,  
        INT cbIndicator,  
        DBINT cbData,  
        LPCBYTE pTerm,  
        INT cbTerm,  
        INT eDataType,  
        INT idxServerCol);  
```  
  
## <a name="arguments"></a>Argumentos

 *hdbc*  
 Es el identificador de la conexión ODBC habilitada para la copia masiva.  
  
 *pData*  
 Es un puntero a los datos copiados. Si *eDataType* es SQLTEXT, SQLNTEXT, SQLXML, SQLUDT, SQLCHARACTER, SQLVARCHAR, SQLVARBINARY, SQLBINARY, SQLNCHAR o SQLIMAGE, *PDATA* puede ser null. Un *PDATA* null indica que los valores de datos largos se enviarán a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en fragmentos mediante [bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md). El usuario solo debe establecer *pdata* en NULL si la columna correspondiente al campo enlazado al usuario es una columna BLOB; de lo contrario **bcp_bind** producirá un error.  
  
 Si en los datos hay indicadores, estos aparecen en la memoria directamente antes de los datos. El parámetro *pdata* apunta a la variable de indicador en este caso y el ancho del indicador, el parámetro *cbIndicator* , se usa en la copia masiva para direccionar los datos del usuario correctamente.  
  
 *cbIndicator*  
 Es la longitud, en bytes, de un indicador de longitud o nulo para los datos de la columna. Los valores de longitud de indicador válidos son 0 (cuando no se utiliza ningún indicador), 1, 2, 4 u 8. Los indicadores aparecen en la memoria directamente antes de ningún dato. Por ejemplo, la siguiente definición de tipo de estructura se puede utilizar para insertar valores enteros en una tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizando la copia masiva:  
  
```
typedef struct tagBCPBOUNDINT  
    {  
    int iIndicator;  
    int Value;  
    } BCPBOUNDINT;  
```  
  
 En el caso de ejemplo, el parámetro *pdata* se establecería en la dirección de una instancia declarada de la estructura, la dirección del miembro de la estructura BCPBOUNDINT *iIndicator* . El parámetro *cbIndicator* se establecería en el tamaño de un entero (sizeof (int)) y el parámetro *cbData* se establecería de nuevo en el tamaño de un entero (sizeof (int)). Para copiar de forma masiva una fila en el servidor que contiene un valor NULL para la columna enlazada, el valor del miembro *iIndicator* de la instancia debe establecerse en SQL_NULL_DATA.  
  
 *cbData*  
 Es el número de bytes de datos de la variable de programa, sin incluir la longitud de ningún terminador o indicador de longitud o nulo.  
  
 Establecer *cbData* en SQL_NULL_DATA significa que todas las filas copiadas en el servidor contienen un valor null para la columna.  
  
 Al establecer *cbData* en SQL_VARLEN_DATA, se indica que el sistema usará un terminador de cadena u otro método para determinar la longitud de los datos copiados.  
  
 En el caso de los tipos de datos de longitud fija, como los enteros, el tipo de datos indica la longitud de los datos al sistema. Por lo tanto, en el caso de los tipos de datos de longitud fija, *cbData* se puede SQL_VARLEN_DATA o la longitud de los datos de forma segura.  
  
 En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] el caso de los tipos de datos de caracteres y binarios, *cbData* puede ser SQL_VARLEN_DATA, SQL_NULL_DATA, algún valor positivo o 0. Si *cbData* es SQL_VARLEN_DATA, el sistema utiliza un indicador de longitud o null (si existe) o una secuencia de terminador para determinar la longitud de los datos. Si se proporciona ambos, el sistema utiliza el que hace que se copie una menor cantidad de datos. Si *cbData* es SQL_VARLEN_DATA, el tipo de datos de la columna es [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] un tipo de carácter o binario y no se especifica un indicador de longitud ni una secuencia de terminador, el sistema devuelve un mensaje de error.  
  
 Si *cbData* es 0 o un valor positivo, el sistema utiliza *cbData* como la longitud de los datos. Sin embargo, si, además de un valor de *cbData* positivo, se proporciona un indicador de longitud o una secuencia de terminador, el sistema determina la longitud de los datos mediante el método que hace que se copie la menor cantidad de datos.  
  
 El valor del parámetro *cbData* representa el recuento de bytes de datos. Si los datos de caracteres se representan mediante caracteres anchos de Unicode, un valor de parámetro *cbData* positivo representa el número de caracteres multiplicado por el tamaño en bytes de cada carácter.  
  
 *pTerm*  
 Es un puntero al modelo de bytes que marca el fin de esta variable de programa, en caso de haberlo. Por ejemplo, las cadenas ANSI y MBCS de C suelen tener un terminador de 1 byte (\0).  
  
 Si no hay ningún terminador para la variable, establezca *pTerm* en NULL.  
  
 Puede utilizar una cadena vacía ("") para designar el terminador nulo de C como el terminador de la variable de programa. Dado que la cadena vacía terminada en NULL constituye un solo byte (el propio byte de terminador), establezca *cbTerm* en 1. Por ejemplo, para indicar que la cadena en *szName* está terminada en NULL y que se debe usar el terminador para indicar la longitud:  
  
```
bcp_bind(hdbc, szName, 0,  
   SQL_VARLEN_DATA, "", 1,  
   SQLCHARACTER, 2)  
```

 Un formulario no terminado de este ejemplo podría indicar que se copian 15 caracteres de la variable *szName* a la segunda columna de la tabla enlazada:  

```
bcp_bind(hdbc, szName, 0, 15,
   NULL, 0, SQLCHARACTER, 2)  
```

 La API de copia masiva realiza la conversión de caracteres Unicode a MBCS según sea necesario. Asegúrese de que tanto la cadena de bytes de terminador como la longitud de la cadena de bytes están correctamente establecidas. Por ejemplo, para indicar que la cadena en *szName* es una cadena de caracteres anchos de Unicode, terminada por el valor de terminador null de Unicode:  
  
```  
bcp_bind(hdbc, szName, 0,
   SQL_VARLEN_DATA, L"",  
   sizeof(WCHAR), SQLNCHAR, 2)  
```  
  
 Si la columna [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] enlazada es un carácter ancho, no se realiza ninguna conversión en [bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md). Si el tipo de caracteres de la columna de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es MBCS, la conversión de caracteres anchos a caracteres multibyte se realiza cuando los datos se envían a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 *cbTerm*  
 Es el número de bytes que hay en el terminador para la variable de programa, si existe. Si no hay ningún terminador para la variable, establezca *cbTerm* en 0.  

*eDataType* Es el tipo de datos C de la variable de programa. Los datos de la variable de programa se convierten al tipo de la columna de base de datos. Si este parámetro es 0, no se realiza ninguna conversión.  

Los *eDataType* tokens de tipo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] datos enumeran el parámetro eDataType en SQLNCLI. h, no los enumeradores de tipos de datos C de ODBC. Por ejemplo, puede especificar un entero de dos bytes, el tipo ODBC SQL_C_SHORT, utilizando el tipo SQLINT2 específico de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  

[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]incorporó la compatibilidad con los tokens de tipo de datos SQLXML y SQLUDT en el parámetro **_eDataType_** .  

En esta tabla se muestran los tipos de datos enumerados válidos y los tipos de datos ODBC C correspondientes.

|eDataType|Tipo de C|
|-----------------------|------------|  
|SQLTEXT|char *|  
|SQLNTEXT|wchar_t *|  
|SQLCHARACTER|char *|  
|SQLBIGCHAR|char *|  
|SQLVARCHAR|char *|  
|SQLBIGVARCHAR|char *|  
|SQLNCHAR|wchar_t *|  
|SQLNVARCHAR|wchar_t *|  
|SQLBINARY|unsigned char *|  
|SQLBIGBINARY|unsigned char *|  
|SQLVARBINARY|unsigned char *|  
|SQLBIGVARBINARY|unsigned char *|  
|SQLBIT|char|  
|SQLBITN|char|  
|SQLINT1|char|  
|SQLINT2|short int|  
|SQLINT4|int|  
|SQLINT8|_int64|  
|SQLINTN|*cbIndicator*<br /> 1: SQLINT1<br /> 2: SQLINT2<br /> 4: SQLINT4<br /> 8: SQLINT8|  
|SQLFLT4|FLOAT|  
|SQLFLT8|FLOAT|  
|SQLFLTN|*cbIndicator*<br /> 4: SQLFLT4<br /> 8: SQLFLT8|  
|SQLDECIMALN|SQL_NUMERIC_STRUCT|  
|SQLNUMERICN|SQL_NUMERIC_STRUCT|  
|SQLMONEY|DBMONEY|  
|SQLMONEY4|DBMONEY4|  
|SQLMONEYN|*cbIndicator*<br /> 4: SQLMONEY4<br /> 8: SQLMONEY|  
|SQLTIMEN|SQL_SS_TIME2_STRUCT|  
|SQLDATEN|SQL_DATE_STRUCT|  
|SQLDATETIM4|DBDATETIM4|  
|SQLDATETIME|DBDATETIME|  
|SQLDATETIMN|*cbIndicator*<br /> 4: SQLDATETIM4<br /> 8: SQLDATETIME|  
|SQLDATETIME2N|SQL_TIMESTAMP_STRUCT|  
|SQLDATETIMEOFFSETN|SQL_SS_TIMESTAMPOFFSET_STRUCT|  
|SQLIMAGE|unsigned char *|  
|SQLUDT|unsigned char *|  
|SQLUNIQUEID|SQLGUID|  
|SQLVARIANT|*Cualquier tipo de datos excepto:*<br />-   text<br />-   ntext<br />-   image<br />-   varchar(max)<br />-   varbinary(max)<br />-   nvarchar(max)<br />-   xml<br />-   timestamp|  
|SQLXML|*Tipos de datos C admitidos:*<br />-   char*<br />-   wchar_t *<br />-   unsigned char *|  

*idxServerCol* Es la posición ordinal de la columna en la tabla de base de datos en la que se copian los datos. La primera columna de una tabla es la columna 1. La posición ordinal de una columna se notifica mediante [SQLColumns](../../relational-databases/native-client-odbc-api/sqlcolumns.md).  
  
## <a name="returns"></a>Devuelve

 SUCCEED o FAIL.

## <a name="remarks"></a>Observaciones

Utilice **bcp_bind** para una manera rápida y eficaz de copiar datos de una variable de programa en una tabla [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]de.  

Llame a [bcp_init](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-init.md) antes de llamar a esta o a cualquier otra función de copia masiva. Al **bcp_init** llamar a bcp_init [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se establece la tabla de destino para la copia masiva. Cuando se llama a **bcp_init** para su uso con **bcp_bind** y [bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md), el parámetro **bcp_init** _szDataFile_ , que indica el archivo de datos, se establece en null; el parámetro **bcp_init**_eDirection_ se establece en DB_IN.  

Realice una llamada de **bcp_bind** independiente para cada columna de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] la tabla en la que desea copiar. Una vez realizadas las llamadas de **bcp_bind** necesarias, llame a **bcp_sendrow** para enviar una fila de datos de las variables de programa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]a. No se permite volver a enlazar una columna.

Siempre que desee [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] confirmar las filas ya recibidas, llame a [bcp_batch](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-batch.md). Por ejemplo, llame a **bcp_batch** una vez por cada 1000 filas insertadas o en cualquier otro intervalo.  

Cuando no haya más filas para insertar, llame a [bcp_done](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-done.md). Si no lo hace, se producirá un error.

La configuración de los parámetros de control, especificada con [bcp_control](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md), no tiene ningún efecto en **bcp_bind** transferencias de filas.  

Si *pdata* para una columna se establece en NULL porque su valor se proporcionará mediante llamadas a [bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md), las columnas subsiguientes con *EDATATYPE* establecido en SQLTEXT, SQLNTEXT, SQLXML, SQLUDT, SQLCHARACTER, SQLVARCHAR, SQLVARBINARY, SQLBINARY, SQLNCHAR o SQLIMAGE también se deben enlazar con *pdata* establecido en null, y sus valores también se deben proporcionar mediante llamadas a **bcp_moretext**.  

En el caso de los nuevos tipos de valores grandes, como **VARCHAR (Max)**, **varbinary (Max)** o **nvarchar (Max)**, puede usar SQLCHARACTER, SQLVARCHAR, SQLVARBINARY, SQLBINARY y SQLNCHAR como indicadores de tipo en el parámetro *eDataType* .  

Si *cbTerm* no es 0, los valores (1, 2, 4 u 8) son válidos para el prefijo (*cbIndicator*). En esta situación, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client buscará el terminador, calculará la longitud de los datos con respecto al terminador (*i*) y establecerá el valor de *cbData* en el valor más pequeño de i y el valor de prefijo.  

Si *cbTerm* es 0 y *cbIndicator* (el prefijo) no es 0, *cbIndicator* debe ser 8. El prefijo de 8 bytes puede tomar los siguientes valores:  

- 0xFFFFFFFFFFFFFFFF significa un valor nulo para el campo.  

- 0xFFFFFFFFFFFFFFFE se trata como un valor de prefijo especial, que se usa para enviar datos de forma eficaz en fragmentos al servidor. El formato de los datos con este prefijo especial es el siguiente:  

- <SPECIAL_PREFIX> \<0 o más fragmentos de datos> <ZERO_CHUNK> donde:  

- PREFIJO_ESPECIAL es 0xFFFFFFFFFFFFFFFE  

- DATA_CHUNK es un prefijo de 4 bytes que contiene la longitud del fragmento, seguido de los datos reales cuya longitud se especifica en el prefijo de 4 bytes.  

- ZERO_CHUNK es un valor de 4 bytes que contiene todos los ceros (00000000) que indican el final de los datos.  

- Cualquier otra longitud válida de 8 bytes se trata como una longitud de datos normal.  

 La llamada a [bcp_columns](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-columns.md) cuando se usa **bcp_bind** produce un error.  
  
## <a name="bcp_bind-support-for-enhanced-date-and-time-features"></a>Compatibilidad de bcp_bind con las características mejoradas de fecha y hora

Para obtener información sobre los tipos utilizados con el parámetro *eDataType* para los tipos de fecha y hora, vea [cambios de copia masiva para tipos de fecha y hora mejorados &#40;OLE DB y ODBC&#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md).  

Para obtener más información, vea [mejoras de fecha y hora &#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  

## <a name="example"></a>Ejemplo
  
```
#include sql.h  
#include sqlext.h  
#include odbcss.h  
// Variables like henv not specified.  
HDBC      hdbc;  
char         szCompanyName[MAXNAME];  
DBINT      idCompany;  
DBINT      nRowsProcessed;  
DBBOOL      bMoreData;  
char*      pTerm = "\t\t";  
  
// Application initiation, get an ODBC environment handle, allocate the  
// hdbc, and so on.  
...
  
// Enable bulk copy prior to connecting on allocated hdbc.  
SQLSetConnectAttr(hdbc, SQL_COPT_SS_BCP, (SQLPOINTER) SQL_BCP_ON,  
   SQL_IS_INTEGER);  
  
// Connect to the data source; return on error.  
if (!SQL_SUCCEEDED(SQLConnect(hdbc, _T("myDSN"), SQL_NTS,  
   _T("myUser"), SQL_NTS, _T("myPwd"), SQL_NTS)))  
   {  
   // Raise error and return.  
   return;  
   }  
  
// Initialize bcp.
if (bcp_init(hdbc, "comdb..accounts_info", NULL, NULL  
   DB_IN) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
// Bind program variables to table columns.
if (bcp_bind(hdbc, (LPCBYTE) &idCompany, 0, sizeof(DBINT), NULL, 0,  
   SQLINT4, 1)    == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
if (bcp_bind(hdbc, (LPCBYTE) szCompanyName, 0, SQL_VARLEN_DATA,  
   (LPCBYTE) pTerm, strnlen(pTerm, sizeof(pTerm)), SQLCHARACTER, 2) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
while (TRUE)  
   {  
   // Retrieve and process program data.
   if ((bMoreData = getdata(&idCompany, szCompanyName)) == TRUE)  
      {  
      // Send the data.
      if (bcp_sendrow(hdbc) == FAIL)  
         {  
         // Raise error and return.  
         return;  
         }  
      }  
   else  
      {  
      // Break out of loop.  
      break;  
      }  
   }  
  
// Terminate the bulk copy operation.  
if ((nRowsProcessed = bcp_done(hdbc)) == -1)  
   {  
   printf_s("Bulk-copy unsuccessful.\n");  
   return;  
   }  
  
printf_s("%ld rows copied.\n", nRowsProcessed);  
```  
  
## <a name="see-also"></a>Consulte también

 [Bulk Copy Functions](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)
