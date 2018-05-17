---
title: bcp_bind | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-extensions-bulk-copy-functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- bcp_bind
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_bind function
ms.assetid: 6e335a5c-64b2-4bcf-a88f-35dc9393f329
caps.latest.revision: 47
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 31f50aa8c094ba983a8382379fd0d833edb0f9dc
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="bcpbind"></a>bcp_bind
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

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
 *HDBC*  
 Es el identificador de la conexión ODBC habilitada para la copia masiva.  
  
 *pData*  
 Es un puntero a los datos copiados. Si *eDataType* es SQLTEXT, SQLNTEXT, SQLXML, SQLUDT, SQLCHARACTER, SQLVARCHAR, SQLVARBINARY, SQLBINARY, SQLNCHAR o SQLIMAGE, *pData* puede ser NULL. Un valor NULL *pData* indica que los valores de datos largos se enviarán a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en fragmentos utilizando [bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md). El usuario solo debe establecer *pData* en NULL si la columna correspondiente al campo enlazado de usuario es una columna BLOB en caso contrario, **bcp_bind** se producirá un error.  
  
 Si en los datos hay indicadores, estos aparecen en la memoria directamente antes de los datos. El *pData* parámetro señala a la variable de indicador en este caso y el ancho del indicador, la *cbIndicator* parámetro, se utiliza la copia masiva para direccionar los datos de usuario correctamente.  
  
 *cbIndicator*  
 Es la longitud, en bytes, de un indicador de longitud o nulo para los datos de la columna. Los valores de longitud de indicador válidos son 0 (cuando no se utiliza ningún indicador), 1, 2, 4 u 8. Los indicadores aparecen en la memoria directamente antes de ningún dato. Por ejemplo, la siguiente definición de tipo de estructura se puede utilizar para insertar valores enteros en una tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizando la copia masiva:  
  
```  
typedef struct tagBCPBOUNDINT  
    {  
    int iIndicator;  
    int Value;  
    } BCPBOUNDINT;  
```  
  
 En el caso del ejemplo, el *pData* parámetro se establecería en la dirección de una instancia declarada de la estructura, la dirección de BCPBOUNDINT *iIndicator* miembro de la estructura. El *cbIndicator* parámetro se establecería en el tamaño de un entero (sizeof y el *cbData* parámetro nuevo se establecería en el tamaño de un entero (sizeof. Para el valor de una fila en el servidor que contiene un valor NULL para la columna dependiente, el valor de la instancia de copia masiva *iIndicator* miembro debe establecerse en SQL_NULL_DATA.  
  
 *cbData*  
 Es el número de bytes de datos de la variable de programa, sin incluir la longitud de ningún terminador o indicador de longitud o nulo.  
  
 Establecer *cbData* en SQL_NULL_DATA, significa que todas las filas copiadas al servidor contienen un valor NULL para la columna.  
  
 Establecer *cbData* en SQL_VARLEN_DATA indica que el sistema utilizará un terminador de cadena o copiado de otro método para determinar la longitud de datos.  
  
 En el caso de los tipos de datos de longitud fija, como los enteros, el tipo de datos indica la longitud de los datos al sistema. Por lo tanto, para los tipos de datos de longitud fija, *cbData* puede ser sin ningún riesgo SQL_VARLEN_DATA o la longitud de los datos.  
  
 Para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] caracteres y tipos de datos binarios, *cbData* puede ser SQL_VARLEN_DATA, SQL_NULL_DATA, algún valor positivo o 0. Si *cbData* es SQL_VARLEN_DATA, el sistema utiliza un indicador de longitud/nulo (si existe) o una secuencia de terminador para determinar la longitud de los datos. Si se proporciona ambos, el sistema utiliza el que hace que se copie una menor cantidad de datos. Si *cbData* es SQL_VARLEN_DATA, el tipo de datos de la columna es una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] caracteres o tipo binario y un indicador de longitud ni una secuencia de terminador no se especifica, el sistema devuelve un mensaje de error.  
  
 Si *cbData* es 0 o un valor positivo, el sistema utiliza *cbData* como la longitud de datos. Sin embargo, si además positivo *cbData* valor, se proporciona una secuencia de indicador o el terminador de longitud, el sistema determina la longitud de datos mediante el método que tiene como resultado la menor cantidad de datos que se va a copiar.  
  
 El *cbData* el valor del parámetro representa el número de bytes de datos. Si los datos de caracteres se representan mediante caracteres anchos de Unicode, positivo *cbData* el valor del parámetro representa el número de caracteres multiplicado por el tamaño en bytes de cada carácter.  
  
 *pTerm*  
 Es un puntero al modelo de bytes que marca el fin de esta variable de programa, en caso de haberlo. Por ejemplo, las cadenas ANSI y MBCS de C suelen tener un terminador de 1 byte (\0).  
  
 Si no hay ningún terminador para la variable, establezca *pTerm* en NULL.  
  
 Puede utilizar una cadena vacía ("") para designar el terminador nulo de C como el terminador de la variable de programa. Dado que la cadena vacía terminada en null constituye un byte único (el propio byte del terminador), establecer *cbTerm* en 1. Por ejemplo, para indicar que la cadena de *szName* termina en null y que se debe utilizar el terminador para indicar la longitud:  
  
```  
bcp_bind(hdbc, szName, 0,  
   SQL_VARLEN_DATA, "", 1,  
   SQLCHARACTER, 2)  
```  
  
 Una forma sin terminación de este ejemplo podría indicar que se copien 15 caracteres de la *szName* variable a la segunda columna de la tabla enlazada:  
  
```  
bcp_bind(hdbc, szName, 0, 15,   
   NULL, 0, SQLCHARACTER, 2)  
```  
  
 La API de copia masiva realiza la conversión de caracteres Unicode a MBCS según sea necesario. Asegúrese de que tanto la cadena de bytes de terminador como la longitud de la cadena de bytes están correctamente establecidas. Por ejemplo, para indicar que la cadena de *szName* es una cadena de caracteres anchos de Unicode, terminada con el valor de terminador nulo de Unicode:  
  
```  
bcp_bind(hdbc, szName, 0,   
   SQL_VARLEN_DATA, L"",  
   sizeof(WCHAR), SQLNCHAR, 2)  
```  
  
 Si el límite [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] la columna es un carácter ancho, se realiza ninguna conversión en [bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md). Si el tipo de caracteres de la columna de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es MBCS, la conversión de caracteres anchos a caracteres multibyte se realiza cuando los datos se envían a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 *cbTerm*  
 Es el número de bytes que hay en el terminador para la variable de programa, si existe. Si no hay ningún terminador para la variable, establezca *cbTerm* en 0.  
  
 *eDataType*  
 Es el tipo de datos de C de la variable de programa. Los datos de la variable de programa se convierten al tipo de la columna de base de datos. Si este parámetro es 0, no se realiza ninguna conversión.  
  
 El *eDataType* parámetro es de tipo enumerado por el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tokens de tipo de datos en sqlncli.h, no los enumeradores de tipo de datos C de ODBC. Por ejemplo, puede especificar un entero de dos bytes, el tipo ODBC SQL_C_SHORT, utilizando el tipo SQLINT2 específico de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] introdujo la compatibilidad con SQLXML y SQLUDT tokens de tipo de datos en el ***eDataType*** parámetro.  
 
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
|SQLFLT4|float|  
|SQLFLT8|float|  
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
  
 *idxServerCol*  
 Es la posición ordinal de la columna en la tabla de base de datos en la que se copian los datos. La primera columna de una tabla es la columna 1. La posición ordinal de una columna se notifica mediante [SQLColumns](../../relational-databases/native-client-odbc-api/sqlcolumns.md).  
  
## <a name="returns"></a>Devuelve  
 SUCCEED o FAIL.  
  
## <a name="remarks"></a>Comentarios  
 Use **bcp_bind** para una forma rápida y eficaz copiar datos de una variable de programa en una tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Llame a [bcp_init](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-init.md) antes de llamar a esta o cualquier otra función de copia masiva. Al llamar a **bcp_init** establece el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabla de destino para la copia masiva. Al llamar a **bcp_init** para su uso con **bcp_bind** y [bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md), **bcp_init** *szDataFile*parámetro, que indica el archivo de datos, se establece en NULL; el **bcp_init *** eDirection* parámetro se establece en DB_IN.  
  
 Asegúrese de otro **bcp_bind** llamar para cada columna en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabla en la que van a copiar. Después de la necesaria **bcp_bind** llamadas se han realizado y después llamar a **bcp_sendrow** para enviar una fila de datos de las variables de programa a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. No se permite volver a enlazar una columna.  
  
 Cada vez que desee [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para confirmar las filas ya recibidas, llame a [bcp_batch](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-batch.md). Por ejemplo, llamar a **bcp_batch** una vez por cada 1000 filas insertadas o en cualquier otro intervalo.  
  
 Cuando no haya más filas para insertar, llame a [bcp_done](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-done.md). Si no lo hace, se producirá un error.  
  
 Controlar la configuración del parámetro especificado con [bcp_control](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md), no tienen ningún efecto **bcp_bind** las transferencias de filas.  
  
 Si *pData* para una columna se establece en NULL porque su valor será proporcionado mediante llamadas a [bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md), las columnas subsiguientes con *eDataType* establecido en SQLTEXT, SQLNTEXT, SQLXML, SQLUDT, SQLCHARACTER, SQLVARCHAR, SQLVARBINARY, SQLBINARY, SQLNCHAR o SQLIMAGE también debe estar enlazado con *pData* establecido en NULL, y sus valores también deben proporcionarse mediante llamadas a **bcp_moretext**.  
  
 Nuevos tipos de valor grande, como **varchar (max)**, **varbinary (max)**, o **nvarchar (max)**, puede utilizar SQLCHARACTER, SQLVARCHAR, SQLVARBINARY, SQLBINARY, y SQLNCHAR como indicadores de tipo en la *eDataType* parámetro.  
  
 Si *cbTerm* es no en 0, cualquier valor (1, 2, 4 o 8) es válido para el prefijo (*cbIndicator*). En esta situación, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client se buscará el terminador, calcular la longitud de los datos en relación con el terminador (*i*) y establezca el *cbData* para el valor más pequeño de i y el valor de prefijo.  
  
 Si *cbTerm* es 0 y *cbIndicator* (el prefijo) no es 0, *cbIndicator* debe ser 8. El prefijo de 8 bytes puede tomar los valores siguientes:  
  
-   0xFFFFFFFFFFFFFFFF significa un valor nulo para el campo.  
  
-   0xFFFFFFFFFFFFFFFE se trata como un valor de prefijo especial que se utiliza para enviar los datos en fragmentos al servidor de forma eficaz. El formato de los datos con este prefijo especial es el siguiente:  
  
-   < prefijo_especial > \<0 o más FRAGMENTOS de datos >< fragmento_cero > donde:  
  
-   PREFIJO_ESPECIAL es 0xFFFFFFFFFFFFFFFE  
  
-   FRAGMENTO_DATOS es un prefijo de 4 bytes que contiene la longitud del fragmento, seguido por los datos reales cuya longitud se especifica en el prefijo de 4 bytes.  
  
-   FRAGMENTO_CERO es un valor de 4 bytes que contiene todos los ceros (00000000) que indican el fin de los datos.  
  
-   Cualquier otra longitud válida de 8 bytes se tratará como una longitud de datos normal.  
  
 Al llamar a [bcp_columns](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-columns.md) al usar **bcp_bind** genera un error.  
  
## <a name="bcpbind-support-for-enhanced-date-and-time-features"></a>Compatibilidad de bcp_bind con las características mejoradas de fecha y hora  
 Para obtener información acerca de los tipos utilizados con el *eDataType* parámetro para los tipos de fecha y hora, vea [cambios en la copia masiva para tipos mejorada de fecha y hora &#40;OLE DB y ODBC&#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md).  
  
 Para obtener más información, consulte [fecha y hora mejoras & #40; ODBC & #41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
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
  
## <a name="see-also"></a>Vea también  
 [Funciones de copia masiva](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
