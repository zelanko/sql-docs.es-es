---
title: bcp_bind | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- bcp_bind
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_bind function
ms.assetid: 6e335a5c-64b2-4bcf-a88f-35dc9393f329
caps.latest.revision: 46
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 118b0a076a4a3f1cc377fc0407f83d1fe23d766c
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37416334"
---
# <a name="bcpbind"></a>bcp_bind
  Enlaza los datos de una variable de programa a una columna de tabla para la copia masiva en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
RETCODE bcp_bind (  
HDBC   
hdbc  
,   
LPCBYTE   
pData  
,  
INT   
cbIndicator  
,  
DBINT   
cbData  
,  
LPCBYTE   
pTerm  
,  
INT   
cbTerm  
,  
INT   
eDataType  
,  
INT   
idxServerCol  
);  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *HDBC*  
 Es el identificador de la conexión ODBC habilitada para la copia masiva.  
  
 *pData*  
 Es un puntero a los datos copiados. Si *eDataType* es SQLTEXT, SQLNTEXT, SQLXML, SQLUDT, SQLCHARACTER, SQLVARCHAR, SQLVARBINARY, SQLBINARY, SQLNCHAR o SQLIMAGE, *pData* puede ser NULL. Un valor NULL *pData* indica que los valores de datos largos se enviarán a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en fragmentos utilizando [bcp_moretext](bcp-moretext.md). El usuario solo debe establecer *pData* en NULL si la columna correspondiente al campo enlazado de usuario es una columna BLOB si no **bcp_bind** se producirá un error.  
  
 Si en los datos hay indicadores, estos aparecen en la memoria directamente antes de los datos. El *pData* parámetro apunta a la variable de indicador en este caso y el ancho del indicador, la *cbIndicator* , se utiliza el parámetro de copia masiva para datos de usuario de la dirección correctamente.  
  
 *cbIndicator*  
 Es la longitud, en bytes, de un indicador de longitud o nulo para los datos de la columna. Los valores de longitud de indicador válidos son 0 (cuando no se utiliza ningún indicador), 1, 2, 4 u 8. Los indicadores aparecen en la memoria directamente antes de ningún dato. Por ejemplo, la siguiente definición de tipo de estructura se puede utilizar para insertar valores enteros en una tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizando la copia masiva:  
  
```  
typedef struct tagBCPBOUNDINT  
    {  
    int iIndicator;  
    int Value;  
    } BCPBOUNDINT;  
```  
  
 En el caso de ejemplo, el *pData* parámetro se establecería en la dirección de una instancia declarada de la estructura, la dirección de BCPBOUNDINT *iIndicator* miembro de estructura. El *cbIndicator* parámetro se establecería en el tamaño de un entero (sizeof y el *cbData* parámetro nuevo se establecería en el tamaño de un entero (sizeof. Para el valor de una fila en el servidor que contiene un valor NULL para la columna dependiente, el valor de la instancia de copia masiva *iIndicator* miembro debe establecerse en SQL_NULL_DATA.  
  
 *cbData*  
 Es el número de bytes de datos de la variable de programa, sin incluir la longitud de ningún terminador o indicador de longitud o nulo.  
  
 Establecer *cbData* en SQL_NULL_DATA, significa que todas las filas copiadas al servidor contienen un valor NULL para la columna.  
  
 Establecer *cbData* en SQL_VARLEN_DATA indica que el sistema utilizará un terminador de cadena o copiado de otro método para determinar la longitud de datos.  
  
 En el caso de los tipos de datos de longitud fija, como los enteros, el tipo de datos indica la longitud de los datos al sistema. Por lo tanto, para los tipos de datos de longitud fija, *cbData* puede ser sin ningún riesgo SQL_VARLEN_DATA o la longitud de los datos.  
  
 Para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] caracteres y tipos de datos binarios, *cbData* puede ser SQL_VARLEN_DATA, SQL_NULL_DATA, algún valor positivo o 0. Si *cbData* es SQL_VARLEN_DATA, el sistema utiliza un indicador de longitud o nulo (si existe) o una secuencia de terminador para determinar la longitud de los datos. Si se proporciona ambos, el sistema utiliza el que hace que se copie una menor cantidad de datos. Si *cbData* es SQL_VARLEN_DATA, el tipo de datos de la columna es una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se especifica el carácter o un tipo binario y no un indicador de longitud ni una secuencia de terminador, el sistema devuelve un mensaje de error.  
  
 Si *cbData* es 0 o un valor positivo, el sistema utiliza *cbData* como la longitud de datos. Sin embargo, si además un positivo *cbData* valor, se proporciona una secuencia de longitud de indicador o un terminador, el sistema determina la longitud de datos mediante el método que da como resultado la menor cantidad de datos que se va a copiar.  
  
 El *cbData* el valor del parámetro representa el recuento de bytes de datos. Si los datos de caracteres se representan mediante caracteres anchos de Unicode, un positivo *cbData* el valor del parámetro representa el número de caracteres multiplicado por el tamaño en bytes de cada carácter.  
  
 *pTerm*  
 Es un puntero al modelo de bytes que marca el fin de esta variable de programa, en caso de haberlo. Por ejemplo, las cadenas ANSI y MBCS de C suelen tener un terminador de 1 byte (\0).  
  
 Si no hay ningún terminador para la variable, establezca *pTerm* en NULL.  
  
 Puede utilizar una cadena vacía ("") para designar el terminador nulo de C como el terminador de la variable de programa. Dado que la cadena vacía terminada en null constituye un solo byte (el propio byte del terminador), establezca *cbTerm* en 1. Por ejemplo, para indicar que la cadena en *szName* está terminada en null y que se debe utilizar el terminador para indicar la longitud:  
  
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
  
 La API de copia masiva realiza la conversión de caracteres Unicode a MBCS según sea necesario. Asegúrese de que tanto la cadena de bytes de terminador como la longitud de la cadena de bytes están correctamente establecidas. Por ejemplo, para indicar que la cadena en *szName* es una cadena de caracteres anchos de Unicode, terminada con el valor de terminador nulo de Unicode:  
  
```  
bcp_bind(hdbc, szName, 0,   
   SQL_VARLEN_DATA, L"",  
   sizeof(WCHAR), SQLNCHAR, 2)  
```  
  
 Si el límite [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] columna es el carácter ancho, no se realiza ninguna conversión en [bcp_sendrow](bcp-sendrow.md). Si el tipo de caracteres de la columna de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es MBCS, la conversión de caracteres anchos a caracteres multibyte se realiza cuando los datos se envían a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 *cbTerm*  
 Es el número de bytes que hay en el terminador para la variable de programa, si existe. Si no hay ningún terminador para la variable, establezca *cbTerm* en 0.  
  
 *eDataType*  
 Es el tipo de datos de C de la variable de programa. Los datos de la variable de programa se convierten al tipo de la columna de base de datos. Si este parámetro es 0, no se realiza ninguna conversión.  
  
 El *eDataType* enumeran el parámetro el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tokens de tipo de datos en sqlncli.h, no los enumeradores de tipo de datos C de ODBC. Por ejemplo, puede especificar un entero de dos bytes, el tipo ODBC SQL_C_SHORT, utilizando el tipo SQLINT2 específico de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] introdujo la compatibilidad con tokens de tipo de datos SQLXML y SQLUDT en el *`eDataType`* parámetro.  
  
 *idxServerCol*  
 Es la posición ordinal de la columna en la tabla de base de datos en la que se copian los datos. La primera columna de una tabla es la columna 1. La posición ordinal de una columna se notifica mediante [SQLColumns](../native-client-odbc-api/sqlcolumns.md).  
  
## <a name="returns"></a>Devuelve  
 SUCCEED o FAIL.  
  
## <a name="remarks"></a>Notas  
 Use **bcp_bind** para una forma rápida y eficaz copiar datos de una variable de programa en una tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Llame a [bcp_init](bcp-init.md) antes de llamar a esta o cualquier otra función de copia masiva. Una llamada a **bcp_init** establece el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabla de destino para la copia masiva. Al llamar a **bcp_init** para su uso con **bcp_bind** y [bcp_sendrow](bcp-sendrow.md), **bcp_init** *szDataFile*parámetro, que indica el archivo de datos, se establece en NULL; el **bcp_init *** eDirection* parámetro se establece en DB_IN.  
  
 Realice otra **bcp_bind** llamar para cada columna de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabla en la que van a copiar. Después de la necesaria **bcp_bind** llamadas se realizaron y, después, llamar a **bcp_sendrow** para enviar una fila de datos desde las variables de programa a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. No se permite volver a enlazar una columna.  
  
 Siempre que desee [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para confirmar las filas ya recibidas, llame a [bcp_batch](bcp-batch.md). Por ejemplo, llamar a **bcp_batch** una vez para cada 1000 filas insertadas o en cualquier otro intervalo.  
  
 Cuando no hay ninguna fila más va a insertar, llame a [bcp_done](bcp-done.md). Si no lo hace, se producirá un error.  
  
 Controlar la configuración del parámetro especificado con [bcp_control](bcp-control.md), no tienen ningún efecto **bcp_bind** las transferencias de filas.  
  
 Si *pData* para una columna se establece en NULL porque su valor será proporcionado mediante llamadas a [bcp_moretext](bcp-moretext.md), las columnas subsiguientes con *eDataType* establecido en SQLTEXT, SQLNTEXT, SQLXML, SQLUDT, SQLCHARACTER, SQLVARCHAR, SQLVARBINARY, SQLBINARY, SQLNCHAR o SQLIMAGE también debe estar enlazado con *pData* establecido en NULL, y sus valores también se deben proporcionar mediante llamadas a `bcp_moretext`.  
  
 Para los nuevos tipos de valor grande, como `varchar(max)`, `varbinary(max)`, o `nvarchar(max)`, puede utilizar SQLCHARACTER, SQLVARCHAR, SQLVARBINARY, SQLBINARY y SQLNCHAR como indicadores de tipo en el *eDataType* parámetro.  
  
 Si *cbTerm* es no en 0, cualquier valor (1, 2, 4 o 8) es válido para el prefijo (*cbIndicator*). En esta situación, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client se buscará el terminador, calcular la longitud de los datos en relación con el terminador (*i*) y establezca el *cbData* al valor más pequeño de i y el valor de prefijo.  
  
 Si *cbTerm* es 0 y *cbIndicator* (el prefijo) no es 0, *cbIndicator* debe ser 8. El prefijo de 8 bytes puede tomar los valores siguientes:  
  
-   0xFFFFFFFFFFFFFFFF significa un valor nulo para el campo.  
  
-   0xFFFFFFFFFFFFFFFE se trata como un valor de prefijo especial que se utiliza para enviar los datos en fragmentos al servidor de forma eficaz. El formato de los datos con este prefijo especial es el siguiente:  
  
-   < prefijo_especial > \<0 o más FRAGMENTOS de datos >< fragmento_cero > donde:  
  
-   PREFIJO_ESPECIAL es 0xFFFFFFFFFFFFFFFE  
  
-   FRAGMENTO_DATOS es un prefijo de 4 bytes que contiene la longitud del fragmento, seguido por los datos reales cuya longitud se especifica en el prefijo de 4 bytes.  
  
-   FRAGMENTO_CERO es un valor de 4 bytes que contiene todos los ceros (00000000) que indican el fin de los datos.  
  
-   Cualquier otra longitud válida de 8 bytes se tratará como una longitud de datos normal.  
  
 Una llamada a [bcp_columns](bcp-columns.md) al usar **bcp_bind** produce un error.  
  
## <a name="bcpbind-support-for-enhanced-date-and-time-features"></a>Compatibilidad de bcp_bind con las características mejoradas de fecha y hora  
 Para obtener información acerca de los tipos utilizados con el *eDataType* parámetro para los tipos de fecha y hora, vea [cambios de copia masiva para tipos mejorada de fecha y hora &#40;OLE DB y ODBC&#41;](../native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md).  
  
 Para obtener más información, consulte [mejoras de fecha y hora &#40;ODBC&#41;](../native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
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
 [Funciones de copia masiva](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
