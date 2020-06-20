---
title: bcp_colfmt | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- bcp_colfmt
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_colfmt function
ms.assetid: 5c3b6299-80c7-4e84-8e69-4ff33009548e
author: rothja
ms.author: jroth
ms.openlocfilehash: 9bcf209096b1929938affcec6a12ce608e54f799
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85019731"
---
# <a name="bcp_colfmt"></a>bcp_colfmt
  Especifica el formato de origen o destino de los datos de un archivo de usuario. Cuando se utiliza como formato de origen, **bcp_colfmt** especifica el formato de un archivo de datos existente utilizado como origen de datos de una copia masiva en una tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Cuando se utiliza como formato de destino, se crea el archivo de datos utilizando los formatos de columna especificados con **bcp_colfmt**.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
RETCODE bcp_colfmt (  
HDBC   
hdbc  
,  
INT  
idxUserDataCol  
,  
BYTE   
eUserDataType  
,  
INT   
cbIndicator  
,  
DBINT   
cbUserData  
,  
LPCBYTE   
pUserDataTerm  
,  
INT   
cbUserDataTerm  
,  
INT   
idxServerCol  
);  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *hdbc*  
 Es el identificador de la conexión ODBC habilitada para la copia masiva.  
  
 *idxUserDataCol*  
 Es el número de columna ordinal del archivo de datos de usuario para el que se especifica el formato. La primera columna es 1.  
  
 *eUserDataType*  
 Es el tipo de datos de esta columna del archivo de usuario. Si es distinto del tipo de datos de la columna correspondiente en la tabla de base de datos (*idxServerColumn*), la copia masiva convierte los datos si es posible.  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]incorporó la compatibilidad con los tokens de tipo de datos SQLXML y SQLUDT en el parámetro *eUserDataType* .  
  
 Los tokens de tipo de datos de *en sqlncli.h enumeran el parámetro* eUserDataType [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , no los enumeradores de tipos de datos C de ODBC. Por ejemplo, puede especificar una cadena de caracteres, tipo SQL_C_CHAR de ODBC, utilizando el tipo SQLCHARACTER específico de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Para especificar la representación de datos predeterminada para el tipo de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , establezca este parámetro en 0.  
  
 Para generar una salida de copia masiva de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en un archivo, cuando *eUserDataType* es SQLDECIMAL o SQLNUMERIC:  
  
-   Si la columna de origen no es **decimal** o **numérica**, se utilizan la precisión y la escala predeterminadas.  
  
-   Si la columna de origen es **decimal** o **numérica**, se utilizan la precisión y la escala de la columna de origen.  
  
 *cbIndicator*  
 Es la longitud, en bytes, de un indicador de longitud o nulo en los datos de columna. Los valores de longitud de indicador válidos son 0 (cuando no se utiliza ningún indicador), 1, 2, 4 u 8.  
  
 Para especificar el uso del indicador de copia masiva predeterminado, establezca este parámetro en SQL_VARLEN_DATA.  
  
 Los indicadores aparecen directamente en memoria antes de cualquier dato y en el archivo de datos directamente antes de los datos a los que se aplican.  
  
 Si se utiliza más de un medio de especificar una longitud de columna del archivo de datos (como un indicador y una longitud máxima de columna o un indicador y una secuencia de terminador) , la copia masiva elige aquél por el que se copia la cantidad mínima de datos.  
  
 Los archivos de datos generados mediante la copia masiva cuando ninguna intervención de usuario ajusta el formato de los datos contienen indicadores acerca de cuándo los datos de columna pueden variar en longitud o cuándo la columna puede aceptar como valores los valores NULL.  
  
 *cbUserData*  
 Es la longitud máxima, en bytes, de los datos de esta columna del archivo de usuario, sin incluir la longitud de los indicadores de longitud o de los terminadores.  
  
 Establecer *cbUserData* en SQL_NULL_DATA indica que todos los valores de columna del archivo de datos son NULL o deben establecerse en NULL.  
  
 Establecer *cbUserData* en SQL_VARLEN_DATA indica que el sistema debe determinar la longitud de datos de cada columna. Para algunas columnas, esto podría significar que se genera un indicador de longitud/nulo para preceder los datos en una copia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]o que se espera el indicador en los datos copiados en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Para los tipos de datos de caracteres y binarios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , *cbUserData* puede ser SQL_VARLEN_DATA, SQL_NULL_DATA, 0 o algún valor positivo. Si *cbUserData* es SQL_VARLEN_DATA, el sistema utiliza un indicador de longitud, si lo hay, o una secuencia de terminador para determinar la longitud de los datos. Si se proporciona un indicador de longitud y una secuencia de terminador, la copia masiva usa aquél por el que se copia la mínima cantidad de datos. Si *cbUserData* es SQL_VARLEN_DATA, el tipo de datos es un tipo de carácter o binario de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y no se especifica ni un indicador de longitud ni una secuencia de terminador, el sistema devuelve un mensaje de error.  
  
 Si *cbUserData* es 0 o un valor positivo, el sistema utiliza *cbUserData* como longitud de datos máxima. Sin embargo, si además de un valor de *cbUserData*positivo, se proporciona un indicador de longitud o una secuencia de terminador, el sistema determina la longitud de los datos utilizando el método por el que se copia la cantidad mínima de datos.  
  
 El valor de *cbUserData* representa el recuento de bytes de datos. Si los datos de caracteres se representan mediante caracteres anchos de Unicode, un valor del parámetro *cbUserData* positivo representa el número de caracteres multiplicado por el tamaño, en bytes, de cada carácter.  
  
 *pUserDataTerm*  
 Es la secuencia de terminador que se va a utilizar para esta columna. Este parámetro es principalmente útil para los tipos de datos de caracteres porque todos los demás tipos son de longitud fija o, en el caso de los datos binarios, requieren un indicador de longitud que grabe con precisión el número de bytes presentes.  
  
 Para evitar la terminación de los datos extraídos o indicar que no se terminen los datos de un archivo de usuario, establezca este parámetro en NULL.  
  
 Si se usa más de un medio para especificar una longitud de columna de usuario (como un terminador y un indicador de longitud, o un terminador y una longitud máxima de columna), la copia masiva elige aquél por el que se copia la cantidad mínima de datos.  
  
 La API de copia masiva realiza la conversión de caracteres Unicode a MBCS según sea necesario. Se deben extremar las precauciones para asegurarse de que se establece correctamente la cadena de bytes del terminador y la longitud de la cadena de bytes.  
  
 *cbUserDataTerm*  
 Es la longitud, en bytes, de la secuencia de terminador que se va a utilizar para esta columna. Si no hay ningún terminador presente o no se desea uno en los datos, establezca este valor en 0.  
  
 *idxServerCol*  
 Es la posición ordinal de la columna de la tabla de base de datos. El primer número de columna es 1. La posición ordinal de una columna se notifica mediante [SQLColumns](../native-client-odbc-api/sqlcolumns.md).  
  
 Si este valor es 0, la copia masiva omite la columna en el archivo de datos.  
  
## <a name="returns"></a>Devoluciones  
 SUCCEED o FAIL.  
  
## <a name="remarks"></a>Comentarios  
 La función **bcp_colfmt** permite especificar el formato de archivo de usuario para las copias masivas. Para la copia masiva, un formato contiene los componentes siguientes:  
  
-   Una asignación de las columnas de archivo de usuario a las columnas de base de datos.  
  
-   El tipo de datos de cada columna del archivo de usuario.  
  
-   La longitud del indicador opcional para cada columna.  
  
-   La longitud máxima de los datos por columna de archivo de usuario.  
  
-   Secuencia de bytes de terminación opcional para cada columna.  
  
-   La longitud de la secuencia de bytes de terminación opcional.  
  
 Cada llamada a **bcp_colfmt** especifica el formato de una columna de archivo de usuario. Por ejemplo, para cambiar la configuración predeterminada de tres columnas de un archivo de datos de usuario de cinco columnas, primero llame a [bcp_columns](bcp-columns.md)**(5)** y, a continuación, llame a **bcp_colfmt** cinco veces, estableciendo con tres de esas llamadas el formato personalizado. Para las dos llamadas restantes, establezca *eUserDataType* en 0 y establezca *cbIndicator*, *cbUserData*y *cbUserDataTerm* en 0, SQL_VARLEN_DATA y 0, respectivamente. Este procedimiento copia las cinco columnas, tres con el formato personalizado y dos con el formato predeterminado.  
  
 Para *cbIndicator*, un valor de 8 para indicar un tipo de valor grande es válido ahora. Si se especifica el prefijo para un campo cuya columna correspondiente es un nuevo tipo max, solamente se puede establecer en 8. Para obtener más información, consulte [bcp_bind](bcp-bind.md).  
  
 Se debe llamar a la función **bcp_columns** antes de realizar cualquier llamada a **bcp_colfmt**.  
  
 Debe llamar a **bcp_colfmt** una vez por cada columna del archivo de usuario.  
  
 La llamada a **bcp_colfmt** más de una vez para cualquier columna de archivo de usuario produce un error.  
  
 No tiene que copiar todos los datos de un archivo de usuario en la tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para omitir una columna, especifique el formato de los datos de la columna; para ello, establezca el parámetro *idxServerCol* en 0. Si desea omitir una columna, debe especificar su tipo.  
  
 La función [bcp_writefmt](bcp-writefmt.md) se puede utilizar para conservar la especificación de formato.  
  
## <a name="bcp_colfmt-support-for-enhanced-date-and-time-features"></a>Compatibilidad de bcp_colfmt con las características mejoradas de fecha y hora  
 Para obtener información acerca de los tipos utilizados con el parámetro *eUserDataType* para los tipos de fecha y hora, vea [cambios de copia masiva para tipos de fecha y hora mejorados &#40;OLE DB y&#41;de ODBC ](../native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md).  
  
 Para obtener más información, vea [mejoras de fecha y hora &#40;ODBC&#41;](../native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="see-also"></a>Consulte también  
 [Bulk Copy Functions](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
