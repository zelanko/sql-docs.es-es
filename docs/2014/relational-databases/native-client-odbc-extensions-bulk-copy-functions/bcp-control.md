---
title: bcp_control | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- bcp_control
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_control function
ms.assetid: 32187282-1385-4c52-9134-09f061eb44f5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 323ea04d32501f04156ffa81452fad5e5cf86664
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62689525"
---
# <a name="bcpcontrol"></a>bcp_control
  Cambia la configuración predeterminada de varios parámetros de control para una copia masiva entre un archivo y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
RETCODE bcp_control (  
HDBC   
hdbc  
,  
INT   
eOption  
,  
void*   
iValue  
);  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *hdbc*  
 Es el identificador de la conexión ODBC habilitada para la copia masiva.  
  
 *eOption*  
 Es uno de los siguientes valores:  
  
 BCPABORT  
 Detiene una operación de copia masiva que ya está en curso. Llame a **bcp_control** con un *eOption* de establecido en BCPABORT desde otro subproceso para detener un ejecución operación de copia de forma masiva. El *iValue* parámetro se omite.  
  
 BCPBATCH  
 Es el número de filas por lote. El valor predeterminado es 0, que indica todas las filas de una tabla, cuando se extraen los datos, o todas las filas del archivo de datos del usuario, cuando los datos se copian en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Un valor inferior a 1 restablece el valor predeterminado para BCPBATCH.  
  
 BCPDELAYREADFMT  
 Un valor booleano, si establece en true, hará que [bcp_readfmt](bcp-readfmt.md) para leer en la ejecución. Si es false (valor predeterminado), bcp_readfmt le inmediatamente leer el archivo de formato. Se producirá un error de secuencia si BCPDELAYREADFMT es true y se llama bcp_columns o bcp_setcolfmt.  
  
 También se producirá un error de secuencia si se llama a `bcp_control(hdbc,` BCPDELAYREADFMT`, (void *)FALSE)` después de llamar a `bcp_control(hdbc,` BCPDELAYREADFMT`, (void *)TRUE)` y bcp_writefmt.  
  
 Para obtener más información, vea [Detección de metadatos](../native-client/features/metadata-discovery.md).  
  
 BCPFILECP  
 *iValue* contiene el número de la página de códigos del archivo de datos. Puede especificar el número de la página de códigos, como 1252 o 850, o uno de estos valores:  
  
 BCPFILE_ACP: los datos en el archivo están en el Windows Microsoft?? página de códigos del cliente.  
  
 BCPFILE_OEMCP: los datos del archivo están en la página de códigos OEM del cliente (valor predeterminado).  
  
 BCPFILE_RAW: los datos del archivo están en la página de códigos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 BCPFILEFMT  
 Número de versión del formato de archivo de datos. Esto puede ser 80 ([!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]), 90 ([!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]), 100 ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] o [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]), 110 ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]), o 120 ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]). 120 es el valor predeterminado. Esto resulta útil para exportar e importar datos en formatos admitidos en versiones anteriores del servidor. Por ejemplo, para importar los datos que se obtienen de una columna de texto en un [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] server en un **varchar (max)** columna en un [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] servidor o posterior, debe especificar 80. De forma similar, si especifica 80 al exportar datos desde un **varchar (max)** columna, éstos se guardarán al igual que las columnas de texto se guardan en el [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] dar formato y se pueden importar a una columna de texto de un [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] server.  
  
 BCPFIRST  
 Es la primera fila de datos del archivo o la tabla que va a copiarse. El valor predeterminado es 1; un valor menor que 1 reinicializa esta opción a su valor predeterminado.  
  
 BCPFIRSTEX  
 En operaciones de salida de BCP, especifica la primera fila de la tabla de base de datos que se copia en el archivo de datos.  
  
 En operaciones de entrada de BCP, especifica la primera fila del archivo de datos que se copia en la tabla de base de datos.  
  
 El *iValue* parámetro debe ser la dirección de un entero de 64 bits con signo que contiene el valor. El valor máximo que puede pasarse a BCPFIRSTEX es 2^63-1.  
  
 BCPFMTXML  
 Especifica que el archivo de formato generado debe estar en formato XML. Está desactivado de forma predeterminada.  
  
 Los archivos con formato XML proporcionan mayor flexibilidad, pero con algunas restricciones más. Por ejemplo, no es posible especificar el prefijo ni el terminador de un campo de forma simultánea, lo que era posible en archivos de formatos anteriores.  
  
> [!NOTE]  
>  Los archivos con formato XML solamente se admiten cuando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se instala junto con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
 BCPHINTS  
 *iValue* contiene un puntero de cadena de caracteres SQLTCHAR. La cadena direccionada especifica sugerencias de procesamiento de copia masiva de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o una instrucción Transact-SQL que devuelve un conjunto de resultados. Si se especifica una instrucción Transact-SQL que devuelve más de un conjunto de resultados, se omiten todos los conjuntos de resultados posteriores al primero. Para obtener más información acerca de las sugerencias de procesamiento de copia masiva, vea [bcp (utilidad)](../../tools/bcp-utility.md).  
  
 BCPKEEPIDENTITY  
 Cuando *iValue* es TRUE, especifica que las funciones de copia masiva insertan valores de datos proporcionados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] las columnas definidas con una restricción de identidad. El archivo de entrada debe proporcionar valores para las columnas de identidad. Si no se establece, se generan nuevos valores de identidad para las filas insertadas. No se tiene en cuenta ningún dato presente en el archivo para las columnas de identidad.  
  
 BCPKEEPNULLS  
 Especifica si los valores de datos vacíos del archivo se convertirán en valores NULL en la tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Cuando *iValue* es TRUE, los valores vacíos se convierten en NULL en la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabla. Con el valor predeterminado, los valores vacíos se convierten en un valor predeterminado para la columna en la tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] si existe un valor predeterminado.  
  
 BCPLAST  
 Es la última fila que va a copiarse. Con el valor predeterminado se copian todas las filas; un valor inferior a 1 restablece esta opción a su valor predeterminado.  
  
 BCPLASTEX  
 En operaciones de salida de BCP, especifica la última fila de la tabla de base de datos que se copia en el archivo de datos.  
  
 En operaciones de entrada de BCP, especifica la última fila del archivo de datos que se copia en la tabla de base de datos.  
  
 El *iValue* parámetro debe ser la dirección de un entero de 64 bits con signo que contiene el valor. El valor máximo que se puede pasar a BCPLASTEX es 2^63-1.  
  
 BCPMAXERRS  
 Es el número de errores permitido antes de que la operación de copia masiva genere un error. El valor predeterminado es 10. un valor menor que 1 restablece esta opción a su valor predeterminado. La copia masiva impone un máximo de 65.535 errores. Si se intenta establecer esta opción en un valor mayor que 65.535, la opción se establece en 65.535.  
  
 BCPODBC  
 Cuando es TRUE, especifica que **datetime** y **smalldatetime** valores guardados en formato de caracteres usará el prefijo de secuencia de escape de marca de tiempo ODBC y el sufijo. La opción BCPODBC solo se aplica a BCP_OUT.  
  
 Cuando sea FALSE, un **datetime** valor que representa el 1 de enero de 1997 se convierte en la cadena de caracteres: 1997-01-01 00:00:00.000. Cuando es TRUE, el mismo **datetime** valor se representa como: {ts ' 1997-01-01 00:00:00.000'}.  
  
 BCPROWCOUNT  
 Devuelve el número de filas afectado por la operación actual (o última) de BCP.  
  
 BCPTEXTFILE  
 Cuando es TRUE, especifica que el archivo de datos es un archivo de texto, en lugar de un archivo binario. Si el archivo es un archivo de texto, BCP determina si es Unicode o no comprobando el marcador de bytes Unicode de los dos primeros bytes del archivo de datos.  
  
 BCPUNICODEFILE  
 Cuando es TRUE, especifica que el archivo de entrada es un archivo Unicode.  
  
 *iValue*  
 Es el valor para el elemento especificado *eOption*. *iValue* se convierte un valor entero (LONGLONG) en un puntero void para permitir la ampliación futura a valores de 64 bits.  
  
## <a name="returns"></a>Devuelve  
 SUCCEED o FAIL.  
  
## <a name="remarks"></a>Comentarios  
 Esta función establece varios parámetros de control para operaciones de copia masiva, incluido el número de errores permitidos antes de cancelar una copia masiva, los números de la primera y la última fila que van a copiarse de un archivo de datos y el tamaño del lote.  
  
 Esta función también se utiliza para especificar la instrucción SELECT cuando la copia masiva del conjunto de resultados de una instrucción SELECT no se realiza desde [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Establecer *eOption* en BCPHINTS y establezca *iValue* para tener un puntero a una cadena SQLTCHAR que contiene la instrucción SELECT.  
  
 Estos parámetros de control solo son significativos cuando la copia se realiza entre un archivo de usuario y una tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Configuración de parámetros de control no tiene ningún efecto en las filas copiadas en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con [bcp_sendrow](bcp-sendrow.md).  
  
## <a name="example"></a>Ejemplo  
  
```  
// Variables like henv not specified.  
SQLHDBC      hdbc;  
DBINT      nRowsProcessed;  
  
// Application initiation, get an ODBC environment handle, allocate the  
// hdbc, and so on.  
...   
  
// Enable bulk copy prior to connecting on allocated hdbc.  
SQLSetConnectAttr(hdbc, SQL_COPT_SS_BCP, (SQLPOINTER) SQL_BCP_ON,  
   SQL_IS_INTEGER);  
  
// Connect to the data source, return on error.  
if (!SQL_SUCCEEDED(SQLConnect(hdbc, _T("myDSN"), SQL_NTS,  
   _T("myUser"), SQL_NTS, _T("myPwd"), SQL_NTS)))  
   {  
   // Raise error and return.  
   return;  
   }  
  
// Initialize bulk copy.   
if (bcp_init(hdbc, _T("address"), _T("address.add"), _T("addr.err"),  
   DB_IN) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
// Set the number of rows per batch.   
if (bcp_control(hdbc, BCPBATCH, (void*) 1000) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
// Set file column count.   
if (bcp_columns(hdbc, 1) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
// Set the file format.   
if (bcp_colfmt(hdbc, 1, 0, 0, SQL_VARLEN_DATA, '\n', 1, 1)  
   == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
// Execute the bulk copy.   
if (bcp_exec(hdbc, &nRowsProcessed) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
printf_s("%ld rows processed by bulk copy.", nRowsProcessed);  
  
```  
  
## <a name="see-also"></a>Vea también  
 [Funciones de copia masiva](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
