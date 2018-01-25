---
title: CREAR formato de archivo externo (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 12/08/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE EXTERNAL FILE FORMAT
- CREATE_EXTERNAL_FILE_FORMAT
dev_langs: TSQL
helpviewer_keywords:
- External
- External, file format
- PolyBase, external file format
ms.assetid: abd5ec8c-1a0e-4d38-a374-8ce3401bc60c
caps.latest.revision: "25"
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: ab389a5c811f915ff497057a5daf12374f1cedb7
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="create-external-file-format-transact-sql"></a>CREAR formato de archivo externo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Crea una definición de formato de archivo externo de PolyBase para datos externos almacenados en Hadoop, el almacenamiento de blobs de Azure o el almacén de Azure Data Lake. Creación de un formato de archivo externo es un requisito previo para crear una tabla externa de PolyBase. Mediante la creación de un formato de archivo externo, especifique el diseño real de los datos que se hace referencia a una tabla externa.  
  
 PolyBase es compatible con los siguientes formatos de archivo:
  
-   Texto delimitado  
  
-   Subárbol RCFile  
  
-   Hive ORC
  
-   Parquet  
  
 Para crear una tabla externa, vea [crear tabla externa &#40; Transact-SQL &#41; ](../../t-sql/statements/create-external-table-transact-sql.md).
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis
  
```
-- Create an external file format for PARQUET files.  
CREATE EXTERNAL FILE FORMAT file_format_name  
WITH (  
    FORMAT_TYPE = PARQUET  
     [ , DATA_COMPRESSION = {  
        'org.apache.hadoop.io.compress.SnappyCodec'  
      | 'org.apache.hadoop.io.compress.GzipCodec'      }  
    ]);  
  
--Create an external file format for ORC files.  
CREATE EXTERNAL FILE FORMAT file_format_name  
WITH (  
    FORMAT_TYPE = ORC  
     [ , DATA_COMPRESSION = {  
        'org.apache.hadoop.io.compress.SnappyCodec'  
      | 'org.apache.hadoop.io.compress.DefaultCodec'      }  
    ]);  
  
--Create an external file format for RCFILE.  
CREATE EXTERNAL FILE FORMAT file_format_name  
WITH (  
    FORMAT_TYPE = RCFILE,  
    SERDE_METHOD = {  
        'org.apache.hadoop.hive.serde2.columnar.LazyBinaryColumnarSerDe'  
      | 'org.apache.hadoop.hive.serde2.columnar.ColumnarSerDe'  
    }  
    [ , DATA_COMPRESSION = 'org.apache.hadoop.io.compress.DefaultCodec' ]);  
  
--Create an external file format for DELIMITED TEXT files.  
CREATE EXTERNAL FILE FORMAT file_format_name  
WITH (  
    FORMAT_TYPE = DELIMITEDTEXT  
    [ , FORMAT_OPTIONS ( <format_options> [ ,...n  ] ) ]  
    [ , DATA_COMPRESSION = {  
           'org.apache.hadoop.io.compress.GzipCodec'  
         | 'org.apache.hadoop.io.compress.DefaultCodec'  
        }  
     ]);  
  
<format_options> ::=  
{  
    FIELD_TERMINATOR = field_terminator  
    | STRING_DELIMITER = string_delimiter  
    | DATE_FORMAT = datetime_format  
    | USE_TYPE_DEFAULT = { TRUE | FALSE } 
    | Encoding = {'UTF8' | 'UTF16'} 
}  
```  
  
## <a name="arguments"></a>Argumentos  
 *file_format_name*  
 Especifica un nombre para el formato de archivo externo.
  
 FORMAT_TYPE especifica el formato de los datos externos.
  
 PARQUET especifica un formato de Parquet.
  
 ORC  
 Especifica un formato optimizado fila columnas (ORC). Esta opción requiere Hive versión 0.11 o superior en el clúster de Hadoop externo. En Hadoop, el formato de archivo ORC ofrece un mejor rendimiento que el formato de archivo RCFILE y la compresión.
  
 RCFILE (en combinación con SERDE_METHOD = *SERDE_method*) especifica un formato de archivo de registro en columnas (RcFile). Esta opción requiere especificar un serializador de Hive y el método deserializador (SerDe). Este requisito es el mismo si usas Hive/HiveQL en Hadoop para consultar RC (archivos). Tenga en cuenta que el método SerDe distingue mayúsculas de minúsculas.
  
 Ejemplos de especificación RCFile con los dos métodos de SerDe PolyBase es compatible con.
  
-   FORMAT_TYPE = RCFILE, SERDE_METHOD = 'org.apache.hadoop.hive.serde2.columnar.LazyBinaryColumnarSerDe'
  
-   FORMAT_TYPE = RCFILE, SERDE_METHOD = 'org.apache.hadoop.hive.serde2.columnar.ColumnarSerDe'
  
 DELIMITEDTEXT especifica un formato de texto con delimitadores de columna, también se denomina terminadores de campo.
  
 FIELD_TERMINATOR = *field_terminator* se aplica solo a los archivos de texto delimitado. El terminador de campo especifica uno o varios caracteres que marcan el final de cada campo (columna) en el archivo de texto delimitado. El valor predeterminado es el ꞌ de carácter de canalización | ꞌ. Para obtener soporte garantizada, se recomienda usar uno o varios caracteres ascii.
  
  
 Ejemplos:  
  
-   FIELD_TERMINATOR = ' |'  
  
-   FIELD_TERMINATOR = ' '  
  
-   FIELD_TERMINATOR = ꞌ\tꞌ  
  
-   FIELD_TERMINATOR = '~|~'  
  
 STRING_DELIMITER = *string_delimiter*  
 Especifica el terminador de campo de datos de tipo cadena en el archivo de texto delimitado. El delimitador de cadenas es uno o más caracteres de longitud y se incluye con comillas simples. El valor predeterminado es una cadena vacía "". Para obtener soporte garantizada, se recomienda usar uno o varios caracteres ascii.
 
  
 Ejemplos:  

-   STRING_DELIMITER = ' "'

-   STRING_DELIMITER = '0 x 22--' hexadecimal del carácter de comilla doble
  
-   STRING_DELIMITER = ' *'  
  
-   STRING_DELIMITER = Ꞌ, Ꞌ  
  
-   STRING_DELIMITER = '0x7E0x7E'--dos tildes (por ejemplo, ~ ~)
  
 FECHA\_formato = *datetime_format* especifica un formato personalizado para todos los datos de fecha y hora en que pueden aparecer en un archivo de texto delimitado. Si el archivo de origen usa formatos de fecha y hora de forma predeterminada, esta opción no es necesaria. Un solo formato de fecha y hora personalizado se permite por archivo. No se puede especificar varios formatos de fecha y hora personalizado por cada archivo. Sin embargo, puede usar varios formatos de fecha y hora, si cada uno de ellos es el formato predeterminado para su tipo de datos correspondiente en la definición de tabla externa.

PolyBase solo utiliza el formato de fecha personalizado para importar los datos. No utiliza el formato personalizado para escribir datos en un archivo externo.

 Cuando DATE_FORMAT no se especifica o es una cadena vacía, PolyBase utiliza los formatos predeterminados siguientes:
  
-   Fecha y hora: 'aaaa-MM-dd hh'  
  
-   SmallDateTime: "aaaa-MM-dd hh: mm"  
  
-   Fecha: 'aaaa-MM-dd'  
  
-   DateTime2: "aaaa-MM-dd hh"  
  
-   DateTimeOffset: "aaaa-MM-dd hh"  
  
-   Tiempo: 'hh'  
  
 **Formatos de fecha de ejemplo** se encuentran en la tabla siguiente.  
  
 Notas acerca de la tabla:  
  
-   Año, mes y día pueden tener una variedad de formatos y pedidos. La tabla muestra solo la **AMD** formato. Mes puede tener 1 o 2 dígitos o 3 caracteres. Día puede tener 1 o 2 dígitos. Año puede tener 2 ó 4 dígitos.
  
-   Milisegundos (fffffff) no es necesario.
  
-   AM, pm (tt) no es necesario. El valor predeterminado es AM.
  
|Date (tipo)|Ejemplo|Description|  
|---------------|-------------|-----------------|  
|DateTime|DATE_FORMAT = "aaaa-MM-dd fff"|Además de año, mes y día, este formato de fecha incluye 00-24 horas, de 00 a 59 minutos, de 00 a 59 segundos y 3 dígitos para milisegundos.|  
|DateTime|DATE_FORMAT = 'aaaa-MM-dd hh:mm:ss.ffftt'|Además de año, mes y día, este formato de fecha incluye 00-12 horas, de 00 a 59 minutos, de 00 a 59 segundos, 3 dígitos para milisegundos y AM, am, PM o pm. |  
|SmallDateTime|DATE_FORMAT = "aaaa-MM-dd hh: mm"|Además de año, mes y día, este formato de fecha incluye 00-23 horas, de 00 a 59 minutos.|  
|SmallDateTime|DATE_FORMAT = 'aaaa-MM-dd hh:mmtt'|Además de año, mes y día, este formato de fecha incluye 11: 00 horas, minutos 00-59, ningún segundos y a. M., am, PM o pm.|  
|Date|DATE_FORMAT =  'yyyy-MM-dd'|Año, mes y día. No se incluye ningún elemento de tiempo.|  
|Date|DATE_FORMAT = "AAAA-MMM-dd"|Año, mes y día. Cuando se especifica el mes con 3 M, el valor de entrada es una o las cadenas de enero, febrero, marzo, abril, mayo, Jun, Jul, Aug, Sep, Oct, Nov o Dec.|  
|datetime2|DATE_FORMAT = 'se ss aaaa-MM-dd. ' fffffff|Además de año, mes y día, este formato de fecha incluye 00-23 horas, de 00 a 59 minutos, de 00 a 59 segundos y 7 dígitos de milisegundos.|  
|datetime2|DATE_FORMAT = 'aaaa-MM-dd hh:mm:ss.ffffffftt'|Además de año, mes y día, este formato de fecha incluye 11: 00 horas, de 00 a 59 minutos, de 00 a 59 segundos, 7 dígitos para milisegundos y AM, am, PM o pm.|  
|DateTimeOffset|DATE_FORMAT = 'aaaa-MM-dd ss. fffffff zzz'|Además de año, mes y día, este formato de fecha incluye 00-23 horas, de 00 a 59 minutos, de 00 a 59 segundos y 7 dígitos para milisegundos y el ajuste de zona horaria que se coloca en el archivo de entrada como `{+&#124;-}HH:ss`. Por ejemplo, desde el momento de Los Ángeles sin horario de verano ahorro es 8 horas anteriores a la hora UTC, un valor de -08:00 en el archivo de entrada especifica la zona horaria de Los Ángeles.|  
|DateTimeOffset|DATE_FORMAT = 'aaaa-MM-dd hh:mm:ss.ffffffftt zzz'|Además de año, mes y día, este formato de fecha incluye 11: 00 horas, de 00 a 59 minutos, de 00 a 59 segundos, 7 dígitos para milisegundos, (a. M., am, PM o p.m.) y el desplazamiento de zona horaria. Vea la descripción de la fila anterior.|  
|Time|DATE_FORMAT = 'Hh'|No hay ningún valor de fecha, solo 00-23 horas, de 00 a 59 minutos y, de 00 a 59 segundos.|  
  
 Todos los formatos de fecha admitidos:
  
|datetime|smalldatetime|date|datetime2|datetimeoffset|  
|--------------|-------------------|----------|---------------|--------------------|  
|[M[M]]M-[d]d-[yy]yy HH:mm:ss[.fff]|[M[M]]M-[d]d-[yy]yy HH:mm[:00]|[M[M]]M-[d]d-[yy]yy|[M[M]]M-[d]d-[yy]yy HH:mm:ss[.fffffff]|[M[M]]M-[d]d-[yy]yy HH:mm:ss[.fffffff] zzz|  
|[M[M]]M-[d]d-[yy]yy hh:mm:ss[.fff][tt]|[M[M]]M-[d]d-[yy]yy hh:mm[:00][tt]||[M[M]]M-[d]d-[yy]yy hh:mm:ss[.fffffff][tt]|[M [M]] M-[d] d-[aa] aa hh [.fffffff] [tt] zzz|  
|[M[M]]M-[yy]yy-[d]d HH:mm:ss[.fff]|[M[M]]M-[yy]yy-[d]d HH:mm[:00]|[M[M]]M-[yy]yy-[d]d|[M[M]]M-[yy]yy-[d]d HH:mm:ss[.fffffff]|[M[M]]M-[yy]yy-[d]d HH:mm:ss[.fffffff] zzz|  
|[M[M]]M-[yy]yy-[d]d hh:mm:ss[.fff][tt]|[M[M]]M-[yy]yy-[d]d hh:mm[:00][tt]||[M[M]]M-[yy]yy-[d]d hh:mm:ss[.fffffff][tt]|[M[M]]M-[yy]yy-[d]d hh:mm:ss[.fffffff][tt] zzz|  
|[yy]yy-[M[M]]M-[d]d HH:mm:ss[.fff]|[yy]yy-[M[M]]M-[d]d HH:mm[:00]|[yy]yy-[M[M]]M-[d]d|[yy]yy-[M[M]]M-[d]d HH:mm:ss[.fffffff]|[yy]yy-[M[M]]M-[d]d HH:mm:ss[.fffffff]  zzz|  
|[yy]yy-[M[M]]M-[d]d hh:mm:ss[.fff][tt]|[yy]yy-[M[M]]M-[d]d hh:mm[:00][tt]||[yy]yy-[M[M]]M-[d]d hh:mm:ss[.fffffff][tt]|[yy]yy-[M[M]]M-[d]d hh:mm:ss[.fffffff][tt] zzz|  
|[yy]yy-[d]d-[M[M]]M HH:mm:ss[.fff]|[yy]yy-[d]d-[M[M]]M HH:mm[:00]|[yy]yy-[d]d-[M[M]]M|[yy]yy-[d]d-[M[M]]M HH:mm:ss[.fffffff]|[yy]yy-[d]d-[M[M]]M HH:mm:ss[.fffffff]  zzz|  
|[yy]yy-[d]d-[M[M]]M hh:mm:ss[.fff][tt]|[yy]yy-[d]d-[M[M]]M hh:mm[:00][tt]||[yy]yy-[d]d-[M[M]]M hh:mm:ss[.fffffff][tt]|[yy]yy-[d]d-[M[M]]M hh:mm:ss[.fffffff][tt] zzz|  
|[d]d-[M[M]]M-[yy]yy HH:mm:ss[.fff]|[d]d-[M[M]]M-[yy]yy HH:mm[:00]|[d]d-[M[M]]M-[yy]yy|[d]d-[M[M]]M-[yy]yy HH:mm:ss[.fffffff]|[d]d-[M[M]]M-[yy]yy HH:mm:ss[.fffffff] zzz|  
|[d]d-[M[M]]M-[yy]yy hh:mm:ss[.fff][tt]|[d]d-[M[M]]M-[yy]yy hh:mm[:00][tt]||[d]d-[M[M]]M-[yy]yy hh:mm:ss[.fffffff][tt]|[d] [M [M]] d-M-[aa] aa hh [.fffffff] [tt] zzz|  
|[d]d-[yy]yy-[M[M]]M HH:mm:ss[.fff]|[d]d-[yy]yy-[M[M]]M HH:mm[:00]|[d]d-[yy]yy-[M[M]]M|[d]d-[yy]yy-[M[M]]M HH:mm:ss[.fffffff]|[d]d-[yy]yy-[M[M]]M HH:mm:ss[.fffffff]  zzz|  
|[d]d-[yy]yy-[M[M]]M hh:mm:ss[.fff][tt]|[d]d-[yy]yy-[M[M]]M hh:mm[:00][tt]||[d]d-[yy]yy-[M[M]]M hh:mm:ss[.fffffff][tt]|[d]d-[yy]yy-[M[M]]M hh:mm:ss[.fffffff][tt] zzz|  
  
 Detalles:  
  
-   Para separar los valores de mes, día y año, puede usar ':', '/' o '. '. Por simplicidad, la tabla utiliza el separador ':'.
  
-   Para especificar el mes como texto, use tres o más caracteres. Meses con 1 o 2 caracteres se interpretan como un número.
  
-   Para separar los valores de hora, use el ': ' símbolo.
  
-   Letras entre corchetes son opcionales.
  
-   Designan las letras "tt" [AM | PM | am | pm]. AM es el valor predeterminado. Cuando se especifica 'tt', el valor de hora (hh) debe estar en el intervalo de 0 a 12.
  
-   Las letras 'zzz' designan el desplazamiento de zona horaria para la zona de horaria actual del sistema en el formato {+ |-} HH:ss].
  
 USE_TYPE_DEFAULT = {TRUE | **FALSE** } especifica cómo controlar los valores que faltan en archivos de texto delimitado cuando PolyBase recupera datos del archivo de texto.
  
 TRUE si al recuperar los datos del archivo de texto, almacenar cada valor que falta mediante el valor predeterminado para el tipo de datos de la columna correspondiente en la definición de tabla externa. Por ejemplo, reemplace un valor que falta con:  
  
-   0 si la columna se define como una columna numérica.
  
-   Una cadena vacía "" si la columna es una columna de cadenas.
  
-   1900-01-01 si la columna es una columna de fecha.
  
 Almacén de FALSE que faltan todos los valores como NULL. Los valores NULL que se almacenan utilizando la palabra NULL en el archivo de texto delimitado se importan como la cadena 'NULL'.
  
   Codificación = {'UTF8' | 'UTF16}' en Azure SQL Data Warehouse, PolyBase puede leer UTF8 y UTF16-LE codificado delimitado por archivos de texto. En SQL Server y PDW, PolyBase no admite leer UTF16 archivos codificados.
  
 DATA_COMPRESSION = *data_compression_method* especifica el método de compresión de datos para los datos externos. Cuando no se especifica DATA_COMPRESSION, el valor predeterminado es datos sin comprimir.
 Para que funcione correctamente, los archivos de Gzip comprimido deben tener la extensión de archivo ".gz".
 
 El tipo de formato DELIMITEDTEXT admite estos métodos de compresión:
  
-   COMPRESIÓN de datos = 'org.apache.hadoop.io.compress.DefaultCodec'
  
-   DATA COMPRESSION = 'org.apache.hadoop.io.compress.GzipCodec'

 El tipo de formato RCFILE es compatible con este método de compresión:
  
-   COMPRESIÓN de datos = 'org.apache.hadoop.io.compress.DefaultCodec'
  
 El tipo de formato de archivo ORC admite estos métodos de compresión:
  
-   COMPRESIÓN de datos = 'org.apache.hadoop.io.compress.DefaultCodec'
  
-   DATA COMPRESSION = 'org.apache.hadoop.io.compress.SnappyCodec'
  
 El tipo de formato de archivo PARQUET admite los métodos de compresión de folliwing:
  
-   DATA COMPRESSION = 'org.apache.hadoop.io.compress.GzipCodec'
  
-   DATA COMPRESSION = 'org.apache.hadoop.io.compress.SnappyCodec'
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso ALTER ANY EXTERNAL FILE FORMAT.
  
## <a name="general-remarks"></a>Notas generales
 El formato de archivo externo es de ámbito de base de datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]. Es el ámbito de servidor en [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
 Las opciones de formato son opcionales y solo se aplican a archivos de texto delimitado.  
  
 Cuando los datos se almacenan en uno de los formatos comprimidos, PolyBase descomprime primero los datos antes de devolver los registros de datos.
  
## <a name="limitations-and-restrictions"></a>Limitaciones y restricciones
  
 El delimitador de filas de archivos de texto delimitados debe ser compatibles con LineRecordReader de Hadoop. Es decir, debe ser '\r', '\n' o '\r\n'. Estos delimitadores no son configurables por el usuario.
  
 Las combinaciones de métodos SerDe compatibles con RCFiles y los métodos de compresión de datos admitidos se enumeran anteriormente en este artículo. No todas las combinaciones se admiten.
  
 El número máximo de consultas simultáneas de PolyBase es 32. Cuando se ejecutan 32 consultas simultáneas, cada consulta puede leer un máximo de 33.000 archivos de la ubicación del archivo externo. La carpeta raíz y cada subcarpeta también cuentan como un archivo. Si el grado de simultaneidad es menor que 32, la ubicación del archivo externo puede contener más de 33.000 archivos.
  
 Debido a la limitación en el número de archivos en la tabla externa, es recomendable que almacene menor de 30.000 archivos en la raíz y las subcarpetas de la ubicación del archivo externo. Además, se recomienda mantener el número de subcarpetas bajo el directorio raíz en un número pequeño. Cuando se hace referencia a demasiados archivos, podría producirse una excepción de memoria insuficiente de máquina Virtual Java.
  
  Cuando se exportan el hecho de exportar datos a Hadoop o almacenamiento de blobs de Azure a través de PolyBase, solo los datos, no el names(metadata) de columna como se define en el comando Crear tabla externa.

## <a name="locking"></a>Bloqueo  
 Toma un bloqueo compartido en el objeto de formato de archivo externo.
  
## <a name="performance"></a>Rendimiento
 Usar archivos comprimidos siempre incluye el equilibrio entre transferir menos datos entre el origen de datos externo y SQL Server al tiempo que aumenta el uso de CPU para comprimir y descomprimir los datos.
  
 Archivos de texto comprimido de gzip no son divisibles. Para mejorar el rendimiento de los archivos de texto de Gzip comprimido, se recomienda generar varios archivos que se almacenan en el mismo directorio en el origen de datos externo. Esto permite que PolyBase leer y descomprimir los datos más rápidos mediante el uso de varios procesos de lector y descompresión. El número ideal de archivos comprimidos es el número máximo de procesos de lector de datos por nodo de proceso. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], el número máximo de procesos de lector de datos es 8 por nodo en la versión actual. En [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], el número máximo de procesos de lector de datos por nodo varía según el SLO. Vea [cargar patrones y estrategias de almacenamiento de datos de SQL de Azure](https://blogs.msdn.microsoft.com/sqlcat/2016/02/06/azure-sql-data-warehouse-loading-patterns-and-strategies/) para obtener más información.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-create-a-delimitedtext-external-file-format"></a>A. Crear un formato de archivo externo DELIMITEDTEXT  
 Este ejemplo crea un formato de archivo externo denominado *textdelimited1* para un archivo de texto delimitado. Las opciones se muestran para el formato de\_opciones especifican que los campos en el archivo deben ir separados con un carácter de barra vertical "|". También se comprime el archivo de texto con el códec de Gzip. Si datos\_compresión no se especifica, se descomprime el archivo de texto.
  
 Para un archivo de texto delimitado, el método de compresión de datos puede ser el valor predeterminado de códec, 'org.apache.hadoop.io.compress.DefaultCodec' o el Gzip códec, 'org.apache.hadoop.io.compress.GzipCodec'.
  
```  
CREATE EXTERNAL FILE FORMAT textdelimited1  
WITH (  
    FORMAT_TYPE = DELIMITEDTEXT,  
    FORMAT_OPTIONS (  
        FIELD_TERMINATOR = '|',  
        DATE_FORMAT = 'MM/dd/yyyy' ),  
    DATA_COMPRESSION = 'org.apache.hadoop.io.compress.GzipCodec'
);  
```  
  
### <a name="b-create-an-rcfile-external-file-format"></a>B. Crear un formato de archivo externo RCFile  
 En este ejemplo se crea un formato de archivo externo para un RCFile que usa el org.apache.hadoop.hive.serde2.columnar.LazyBinaryColumnarSerDe de método de serialización/deserialización. También especifica si desea utilizar el códec predeterminado para el método de compresión de datos. Si no se especifica DATA_COMPRESSION, el valor predeterminado no es compresión.
  
```  
CREATE EXTERNAL FILE FORMAT rcfile1  
WITH (  
    FORMAT_TYPE = RCFILE,  
    SERDE_METHOD = 'org.apache.hadoop.hive.serde2.columnar.LazyBinaryColumnarSerDe',  
    DATA_COMPRESSION = 'org.apache.hadoop.io.compress.DefaultCodec'  
);  
```  
  
### <a name="c-create-an-orc-external-file-format"></a>C. Crear un formato de archivo externo ORC  
 Este ejemplo crea un formato de archivo externo de un archivo ORC que comprime los datos con el método de compresión de datos de org.apache.io.compress.SnappyCodec. Si no se especifica DATA_COMPRESSION, el valor predeterminado no es compresión.
  
```  
CREATE EXTERNAL FILE FORMAT orcfile1  
WITH (  
    FORMAT_TYPE = ORC,  
    DATA_COMPRESSION = 'org.apache.hadoop.io.compress.SnappyCodec'  
);  
```  
  
### <a name="d-create-a-parquet-external-file-format"></a>D. Crear un formato de archivo externo PARQUET  
 Este ejemplo crea un formato de archivo externo para un archivo Parquet que comprime los datos con el método de compresión de datos de org.apache.io.compress.SnappyCodec. Si no se especifica DATA_COMPRESSION, el valor predeterminado no es compresión.  
  
```  
CREATE EXTERNAL FILE FORMAT parquetfile1  
WITH (  
    FORMAT_TYPE = PARQUET,  
    DATA_COMPRESSION = 'org.apache.hadoop.io.compress.SnappyCodec'  
);  
```  
  
## <a name="see-also"></a>Vea también
 [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)   
 [CREATE EXTERNAL TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)   
 [CREAR AS de tabla externa SELECT &#40; Transact-SQL &#41;](../../t-sql/statements/create-external-table-as-select-transact-sql.md)   
 [Crear tabla como SELECT &#40; Almacenamiento de datos SQL de Azure &#41;](../../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)   
 [sys.external_file_formats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-file-formats-transact-sql.md)  
