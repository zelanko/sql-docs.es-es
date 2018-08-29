---
title: bcp_setcolfmt | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- bcp_setcolfmt
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_setcolfmt function
ms.assetid: afb47987-39e7-4079-ad66-e0abf4d4c72b
caps.latest.revision: 36
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 93b7518645eb48c36f520dd06f0804ce3e190c32
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43072901"
---
# <a name="bcpsetcolfmt"></a>bcp_setcolfmt
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  El **bcp_setcolfmt** función reemplaza la [bcp_colfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-colfmt.md). Para especificar la intercalación de columna, se debe usar la función **bcp_setcolfmt** . [bcp_setbulkmode](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-setbulkmode.md) puede utilizarse para especificar más de un formato de columna.  
  
 Esta función proporciona un enfoque flexible para especificar el formato de columna en una operación de copia masiva. Se utiliza para establecer los atributos de formato de columna individuales. Cada llamada a **bcp_setcolfmt** establece un atributo de formato de columna.  
  
 La función **bcp_setcolfmt** especifica el formato de origen o de destino de los datos de un archivo de usuario. Cuando se utiliza como formato de origen, **bcp_setcolfmt** especifica el formato de un archivo de datos existente utilizado como un origen de datos de una copia masiva en una tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Cuando se utiliza como formato de destino, se crea el archivo de datos utilizando los formatos de columna especificados con **bcp_setcolfmt**.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
RETCODE bcp_setcolfmt (  
        HDBC hdbc,  
        INT field,  
        INT property,  
        void* pValue,  
        INT cbValue);  
```  
  
## <a name="arguments"></a>Argumentos  
 *HDBC*  
 Es el identificador de la conexión ODBC habilitada para la copia masiva.  
  
 *field*  
 Es el número de columnas ordinal para el que se establece la propiedad.  
  
 *property*  
 Es una de las constantes de propiedad. Las constantes de propiedad se definen en esta tabla.  
  
|propiedad|Valor|Descripción|  
|--------------|-----------|-----------------|  
|BCP_FMT_TYPE|BYTE|Es el tipo de datos de esta columna del archivo de usuario. Si es distinto del tipo de datos de la columna correspondiente de la tabla de base de datos, la copia masiva convierte los datos si es posible.<br /><br /> Los tokens de tipo de datos de SQL Server enumeran el parámetro BCP_FMT_TYPE en sqlncli.h, en lugar de los enumeradores de tipo de datos de ODBC C. Por ejemplo, puede especificar una cadena de caracteres, tipo SQL_C_CHAR de ODBC, utilizando el tipo específico SQLCHARACTER de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Para especificar la representación de datos predeterminada para el tipo de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], establezca este parámetro en 0.<br /><br /> Para una copia masiva de SQL Server en un archivo, cuando BCP_FMT_TYPE es SQLDECIMAL o SQLNUMERIC, si la columna de origen no es **decimal** o **numérico**, se utilizan la precisión y escala predeterminadas. En caso contrario, si la columna de origen **decimal** o **numérico**, se utilizan la precisión y escala de la columna de origen.|  
|BCP_FMT_INDICATOR_LEN|INT|Es la longitud en bytes del indicador (prefijo).<br /><br /> Es la longitud, en bytes, de un indicador de longitud o nulo en los datos de columna. Los valores de longitud de indicador válidos son 0 (cuando no se utiliza ningún indicador), 1, 2 ó 4.<br /><br /> Para especificar el uso del indicador de copia masiva predeterminado, establezca este parámetro en SQL_VARLEN_DATA.<br /><br /> Los indicadores aparecen directamente en memoria antes de cualquier dato y en el archivo de datos directamente antes de los datos a los que se aplican.<br /><br /> Si se utiliza más de un medio de especificar una longitud de columna del archivo de datos (como un indicador y una longitud máxima de columna o un indicador y una secuencia de terminador) , la copia masiva elige aquél por el que se copia la cantidad mínima de datos.<br /><br /> Los archivos de datos generados mediante la copia masiva cuando ninguna intervención de usuario ajusta el formato de los datos contienen indicadores acerca de cuándo los datos de columna pueden variar en longitud o cuándo la columna puede aceptar como valores los valores NULL.|  
|BCP_FMT_DATA_LEN|DBINT|Es la longitud en bytes de los datos (longitud de columna).<br /><br /> Es la longitud máxima, en bytes, de los datos de esta columna del archivo de usuario, sin incluir la longitud de los indicadores de longitud o terminadores.<br /><br /> Establecer BCP_FMT_DATA_LEN en SQL_NULL_DATA indica que todos los valores de columna del archivo de datos son NULL o deben establecerse en NULL.<br /><br /> Establecer BCP_FMT_DATA_LEN en SQL_VARLEN_DATA indica que el sistema debe determinar la longitud de los datos de cada columna. Para algunas columnas, esto podría significar que se genera un indicador de longitud/nulo para preceder los datos en una copia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o que se espera el indicador en los datos copiados en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Para los tipos de datos de caracteres y binarios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)],  BCP_FMT_DATA_LEN puede ser SQL_VARLEN_DATA, SQL_NULL_DATA, algún valor positivo o 0. Si BCP_FMT_DATA_LEN  es SQL_VARLEN_DATA, el sistema utiliza un indicador de longitud, si lo hay, o una secuencia de terminador para determinar la longitud de los datos. Si se proporciona un indicador de longitud y una secuencia de terminador, la copia masiva usa aquél por el que se copia la mínima cantidad de datos. Si BCP_FMT_DATA_LEN es SQL_VARLEN_DATA, el tipo de datos es carácter o binario de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y no se especifica un indicador de longitud ni una secuencia de terminador, el sistema devuelve un mensaje de error.<br /><br /> Si BCP_FMT_DATA_LEN es 0 o un valor positivo, el sistema utiliza BCP_FMT_DATA_LEN como la longitud máxima de los datos. Sin embargo, si además de un valor de BCP_FMT_DATA_LEN positivo, se proporciona un indicador de longitud o una secuencia de terminador, el sistema determina la longitud de los datos mediante el método por el cuál se copia la mínima cantidad de datos.<br /><br /> El valor de BCP_FMT_DATA_LEN representa el recuento de bytes de datos. Si los datos de caracteres se representan mediante caracteres anchos de Unicode, un valor del parámetro BCP_FMT_DATA_LEN positivo representa el número de caracteres multiplicado por el tamaño, en bytes, de cada carácter.|  
|BCP_FMT_TERMINATOR|LPCBYTE|Puntero al flujo de terminador (ANSI o Unicode según corresponda) que se va a utilizar para esta columna. Este parámetro es principalmente útil para los tipos de datos de caracteres porque todos los demás tipos son de longitud fija o, en el caso de los datos binarios, requieren un indicador de longitud que grabe con precisión el número de bytes presentes.<br /><br /> Para evitar la terminación de los datos extraídos o indicar que no se terminen los datos de un archivo de usuario, establezca este parámetro en NULL.<br /><br /> Si se usa más de un medio para especificar una longitud de columna de usuario (como un terminador y un indicador de longitud, o un terminador y una longitud máxima de columna), la copia masiva elige aquél por el que se copia la cantidad mínima de datos.<br /><br /> La API de copia masiva realiza la conversión de caracteres Unicode a MBCS según sea necesario. Se deben extremar las precauciones para asegurarse de que se establece correctamente la cadena de bytes del terminador y la longitud de la cadena de bytes.|  
|BCP_FMT_SERVER_COL|INT|Posición ordinal de la columna en la base de datos.|  
|BCP_FMT_COLLATION|LPCSTR|Nombre de intercalación.|  
  
 *pValue*  
 Es el puntero al valor que se va a asociar a la *property*. Permite establecer cada propiedad de formato de columna individualmente.  
  
 *cbValue*  
 Es la longitud del búfer de propiedad en bytes.  
  
## <a name="returns"></a>Devuelve  
 SUCCEED o FAIL.  
  
## <a name="remarks"></a>Notas  
 Esta función reemplaza la función **bcp_colfmt** . Toda la funcionalidad de **bcp_colfmt** se proporciona en la función **bcp_setcolfmt** . Además, también se proporciona compatibilidad con la intercalación de columna. Se recomienda que los atributos de formato de columna siguientes se establezcan en el orden proporcionado a continuación:  
  
 BCP_FMT_SERVER_COL  
  
 BCP_FMT_DATA_LEN  
  
 BCP_FMT_TYPE  
  
 La función **bcp_setcolfmt** le permite especificar el formato de archivo de usuario para las copias masivas. Para la copia masiva, un formato contiene los componentes siguientes:  
  
-   Una asignación de las columnas de archivo de usuario a las columnas de base de datos.  
  
-   El tipo de datos de cada columna del archivo de usuario.  
  
-   La longitud del indicador opcional para cada columna.  
  
-   La longitud máxima de los datos por columna de archivo de usuario.  
  
-   Secuencia de bytes de terminación opcional para cada columna.  
  
-   La longitud de la secuencia de bytes de terminación opcional.  
  
 Cada llamada a **bcp_setcolfmt** especifica el formato de una columna de archivo de usuario. Por ejemplo, para cambiar la configuración predeterminada de tres columnas de un archivo de datos de usuario de cinco columnas, primero llame a [bcp_columns](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-columns.md)**(5)** y, a continuación, llame a **bcp_setcolfmt** cinco veces, con tres de cuyas llamadas establecerá el formato personalizado. Para las dos llamadas restantes, establezca BCP_FMT_TYPE en 0 y establezca respectivamente BCP_FMT_INDICATOR_LENGTH, BCP_FMT_DATA_LEN y *cbValue* en 0, SQL_VARLEN_DATA y 0. Este procedimiento copia las cinco columnas, tres con el formato personalizado y dos con el formato predeterminado.  
  
 Se debe llamar a la función **bcp_columns** antes de llamar a **bcp_setcolfmt**.  
  
 Debe llamar una vez a **bcp_setcolfmt** para cada propiedad de cada columna del archivo de usuario.  
  
 No tiene que copiar todos los datos de un archivo de usuario en la tabla de SQL Server. Para omitir una columna, especifique el formato de los datos de la columna, para ello establezca el parámetro BCP_FMT_SERVER_COL en 0. Si desea omitir una columna, debe especificar su tipo.  
  
 El [bcp_writefmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-writefmt.md) función se puede usar para conservar la especificación de formato.  
  
## <a name="bcpsetcolfmt-support-for-enhanced-date-and-time-features"></a>bcp_setcolfmt admite las características mejoradas de fecha y hora  
 Los tipos utilizados con la propiedad BCP_FMT_TYPE para los tipos de fecha y hora son como se especifica en [cambios de copia masiva para tipos mejorada de fecha y hora &#40;OLE DB y ODBC&#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md).  
  
 Para obtener más información, consulte [mejoras de fecha y hora &#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="see-also"></a>Vea también  
 [Funciones de copia masiva](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
