---
title: BULK INSERT (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 01/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- BULK_TSQL
- BULK INSERT
- BULK_INSERT_TSQL
- BULK
dev_langs: TSQL
helpviewer_keywords:
- tables [SQL Server], importing data into
- inserting files
- views [SQL Server], importing data into
- BULK INSERT statement
- views [SQL Server], exporting data from
- importing data, bulk import
- bulk importing [SQL Server], BULK INSERT statement
- file importing [SQL Server]
ms.assetid: be3984e1-5ab3-4226-a539-a9f58e1e01e2
caps.latest.revision: "153"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: da5449283269e7ff018e7a4b394eb4c26b69e590
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="bulk-insert-transact-sql"></a>BULK INSERT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Importa un archivo de datos en una tabla o vista de base de datos con un formato especificado por el usuario en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
BULK INSERT   
   [ database_name . [ schema_name ] . | schema_name . ] [ table_name | view_name ]   
      FROM 'data_file'   
     [ WITH   
    (   
   [ [ , ] BATCHSIZE = batch_size ]   
   [ [ , ] CHECK_CONSTRAINTS ]   
   [ [ , ] CODEPAGE = { 'ACP' | 'OEM' | 'RAW' | 'code_page' } ]   
   [ [ , ] DATAFILETYPE =   
      { 'char' | 'native'| 'widechar' | 'widenative' } ]   
   [ [ , ] DATASOURCE = 'data_source_name' ]
   [ [ , ] ERRORFILE = 'file_name' ]
   [ [ , ] ERRORFILE_DATASOURCE = 'data_source_name' ]   
   [ [ , ] FIRSTROW = first_row ]   
   [ [ , ] FIRE_TRIGGERS ]   
   [ [ , ] FORMATFILE_DATASOURCE = 'data_source_name' ]
   [ [ , ] KEEPIDENTITY ]   
   [ [ , ] KEEPNULLS ]   
   [ [ , ] KILOBYTES_PER_BATCH = kilobytes_per_batch ]   
   [ [ , ] LASTROW = last_row ]   
   [ [ , ] MAXERRORS = max_errors ]   
   [ [ , ] ORDER ( { column [ ASC | DESC ] } [ ,...n ] ) ]   
   [ [ , ] ROWS_PER_BATCH = rows_per_batch ]   
   [ [ , ] ROWTERMINATOR = 'row_terminator' ]   
   [ [ , ] TABLOCK ]   

   -- input file format options
   [ [ , ] FORMAT = 'CSV' ]
   [ [ , ] FIELDQUOTE = 'quote_characters']
   [ [ , ] FORMATFILE = 'format_file_path' ]   
   [ [ , ] FIELDTERMINATOR = 'field_terminator' ]   
   [ [ , ] ROWTERMINATOR = 'row_terminator' ]   
    )]   
```  
  
## <a name="arguments"></a>Argumentos  
 *database_name*  
 Es el nombre de base de datos en el que reside la tabla o vista especificada. Si no se especifica, es la base de datos actual.  
  
 *schema_name*  
 Es el nombre del esquema de la tabla o vista. *schema_name* es opcional si el esquema predeterminado para el usuario que realiza la operación de importación masiva es el esquema de la tabla o vista especificada. Si *esquema* no se especifica y el esquema predeterminado del usuario que realiza la operación de importación masiva es diferente de la tabla o vista especificada, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devuelve un mensaje de error y la operación de importación masiva se cancela.  
  
 *table_name*  
 Es el nombre de la tabla o vista en la que se va a realizar una importación masiva de datos. Solo se pueden utilizar vistas en las que todas las columnas hagan referencia a la misma tabla base. Para obtener más información acerca de las restricciones para cargar datos en vistas, consulte [INSERT &#40; Transact-SQL &#41; ](../../t-sql/statements/insert-transact-sql.md).  
  
 **'** *data_file* **'**  
 Es la ruta de acceso completa al archivo de datos que contiene los datos que se van a importar en la tabla o vista especificada. BULK INSERT puede importar datos desde un disco (incluidos una ubicación de red, disquete, disco duro, etc.).   
 
 *data_file* debe especificar una ruta de acceso válida desde el servidor en el que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está ejecutando. Si *data_file* es un equipo remoto, especifique el nombre de convención de nomenclatura universal (UNC, Universal Naming Convention). Un nombre UNC tiene el formato \\ \\ *Systemname*\\*ShareName*\\*ruta de acceso* \\ *FileName*. Por ejemplo, `\\SystemX\DiskZ\Sales\update.txt`.   
**Se aplica a:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
A partir de [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP1.1, que puede ser el data_file en el almacenamiento de blobs de Azure.

**'** *data_source_name* **'**   
**Se aplica a:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
Un origen de datos externo con nombre apunta a la ubicación de almacenamiento de blobs de Azure del archivo que se va a importar. El origen de datos externo debe crearse con el `TYPE = BLOB_STORAGE` opción se ha agregado en [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 1.1 CTP. Para obtener más información, consulte [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md).    
  
 BATCHSIZE  **=**  *batch_size*  
 Especifica el número de filas de un lote. Cada lote se copia en el servidor como una transacción. Si no ocurre así, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] confirma o revierte la transacción de cada lote. De forma predeterminada, todos los datos del archivo de datos especificado componen un lote. Para obtener información acerca de consideraciones de rendimiento, vea la sección "Comentarios" más adelante en este tema.  
  
 CHECK_CONSTRAINTS  
 Especifica que deben comprobarse todas las restricciones de la tabla o vista de destino durante la operación de importación masiva. Sin la opción CHECK_CONSTRAINTS, se omiten las restricciones CHECK y FOREIGN KEY, y, después de la operación, la restricción sobre la tabla se marca como de no confianza.  
  
> [!NOTE]  
>  Las restricciones UNIQUE y PRIMARY KEY se aplican siempre. Cuando se importa en una columna de caracteres definida con la restricción NOT NULL, BULK INSERT inserta una cadena vacía cuando no hay valor en el archivo de texto.  
  
 En algún momento, debe examinar las restricciones de toda la tabla. Si la tabla no estaba vacía antes de la operación de importación masiva, el costo de revalidar la restricción puede superar del costo de aplicar restricciones CHECK a los datos incrementales.  
  
 Una situación en la que quizá desee que las restricciones estén deshabilitadas (comportamiento predeterminado) es si los datos de entrada contienen filas que infringen las restricciones. Con las restricciones CHECK deshabilitadas, puede importar los datos y utilizar después instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] para quitar los datos no válidos.  
  
> [!NOTE]  
>  La opción MAXERRORS no se aplica a la comprobación de restricciones.  
  
 Página de códigos  **=**  { **'**ACP**'** | **'**OEM**'**  |  **'**RAW**'** | **'***página_de_códigos***'** }  
 Especifica la página de códigos de los datos incluidos en el archivo de datos. CODEPAGE solo es pertinente si los datos contienen **char**, **varchar**, o **texto** columnas con valores de caracteres mayores que **127** o menos que **32**.  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)]recomienda que especifique un nombre de intercalación para cada columna de un [archivo de formato](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md).  
  
|Valor de CODEPAGE|Description|  
|--------------------|-----------------|  
|ACP|Columnas de **char**, **varchar**, o **texto** tipo de datos se convierten desde la [!INCLUDE[vcpransi](../../includes/vcpransi-md.md)] / [!INCLUDE[msCoName](../../includes/msconame-md.md)] página de códigos de Windows (ISO 1252) a la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] página de códigos.|  
|OEM (valor predeterminado)|Columnas de **char**, **varchar**, o **texto** tipo de datos se convierten desde la página de códigos OEM del sistema a la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] página de códigos.|  
|RAW|No se realiza ninguna conversión de una página de códigos a otra; se trata de la opción más rápida.|  
|*code_page*|Número específico de una página de códigos; por ejemplo, 850.<br /><br /> **\*\*Importante \* \***  versiones anteriores a [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] no son compatibles con la página de códigos 65001 (codificación UTF-8).|  
  
 DATAFILETYPE  **=**  { **'char'** | **'native'** | **'widechar'**  |  **'widenative'** }  
 Especifica que BULK INSERT realiza la operación de importación con el valor de tipo de archivo de datos especificado.  
  
|Valor de DATAFILETYPE|Todos los datos representados en:|  
|------------------------|------------------------------|  
|**char** (valor predeterminado)|Formato de caracteres.<br /><br /> Para obtener más información, vea [Usar el formato de caracteres para importar o exportar datos &#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md).|  
|**nativo**|Tipos de datos nativos (base de datos). Cree el archivo de datos nativos mediante la importación masiva de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante la **bcp** utilidad.<br /><br /> El valor native ofrece una alternativa de mayor rendimiento al valor char.<br /><br /> Para obtener más información, vea [Usar el formato nativo para importar o exportar datos &#40;SQL Server&#41;](../../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md).|  
|**widechar**|Caracteres Unicode.<br /><br /> Para obtener más información, vea [Usar el formato de caracteres Unicode para importar o exportar datos &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md).|  
|**widenative**|Tipos de datos nativos (base de datos), excepto en **char**, **varchar**, y **texto** columnas, en el que los datos se almacenan como Unicode. Crear el **widenative** importación masiva de datos de archivo de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante la **bcp** utilidad.<br /><br /> El **widenative** valor ofrece una alternativa de mayor rendimiento a **widechar**. Si el archivo de datos contiene [!INCLUDE[vcpransi](../../includes/vcpransi-md.md)] caracteres extendidos, especifique **widenative**.<br /><br /> Para obtener más información, vea [Usar el formato nativo Unicode para importar o exportar datos &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md).|  
  
  ERRORFILE **='***file_name***'**  
 Especifica el archivo utilizado para recopilar filas que tienen errores de formato y no pueden convertirse en un conjunto de filas OLE DB. Estas filas se copian en este archivo de errores desde el archivo de datos "tal cual".  
  
 El archivo de errores se crea cuando se ejecuta el comando. Se produce un error si el archivo ya existe. Además, se crea un archivo de control con la extensión .ERROR.txt. Este archivo hace referencia a cada fila del archivo de errores y proporciona diagnósticos de errores. Tan pronto como se corrigen los errores, se pueden cargar los datos.   
**Se aplica a:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.
A partir de [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)], el `error_file_path` puede estar en el almacenamiento de blobs de Azure.

'errorfile_data_source_name'   
**Se aplica a:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.
Un origen de datos externo con nombre apunta a la ubicación de almacenamiento de blobs de Azure del archivo de error que contendrá los errores encontrados durante la importación. El origen de datos externo debe crearse con el `TYPE = BLOB_STORAGE` opción se ha agregado en [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 1.1 CTP. Para obtener más información, consulte [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md).
 
 FIRSTROW  **=**  *first_row*  
 Especifica el número de la primera fila que se va a cargar. El valor predeterminado es la primera fila del archivo de datos especificado. FIRSTROW está en base 1.  
  
> [!NOTE]  
>  El atributo FIRSTROW no está pensado para saltar los encabezados de columna. La instrucción BULK INSERT no permite omitir los encabezados. Al omitir filas, [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] solo analiza los terminadores de campo y no valida los datos en los campos de las filas omitidas.  
  
 FIRE_TRIGGERS  
 Especifica que se ejecutarán todos los desencadenadores de inserción definidos en la tabla de destino durante la operación de importación masiva. Si se definen desencadenadores para operaciones INSERT en la tabla de destino, se activan para cada lote completado.  
  
 Si no se especifica FIRE_TRIGGERS, no se ejecuta ningún desencadenador de inserción.  

FORMATFILE_DATASOURCE  **=**  'data_source_name'   
**Se aplica a:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 1.1.   
Un origen de datos externo con nombre apunta a la ubicación de almacenamiento de blobs de Azure del archivo de formato que define el esquema de los datos importados. El origen de datos externo debe crearse con el `TYPE = BLOB_STORAGE` opción se ha agregado en [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 1.1 CTP. Para obtener más información, consulte [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md).
  
 KEEPIDENTITY  
 Especifica que se usará el valor o valores de identidad del archivo de datos importado para la columna de identidad. Si no se especifica KEEPIDENTITY, los valores de identidad de esta columna se comprueban pero no se importan y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] asigna automáticamente valores únicos basados en los valores de inicialización y de incremento especificados durante la creación de la tabla. Si el archivo de datos no contiene valores para la columna de identidad de la tabla o vista, utilice un archivo de formato para especificar que se debe omitir la columna de identidad de la tabla o vista cuando se importen los datos; [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] asigna automáticamente valores únicos para la columna. Para obtener más información, vea [DBCC CHECKIDENT &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkident-transact-sql.md).  
  
 Para obtener más información, consulte acerca de cómo mantener identificar valores vea [mantener identidad valores importaciones masivas de datos &#40; SQL Server &#41; ](../../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md).  
  
 KEEPNULLS  
 Especifica que las columnas vacías deben conservar un valor NULL durante la operación de importación masiva, en lugar de tener valores predeterminados para las columnas insertadas. Para obtener más información, vea [Mantener valores NULL o usar valores predeterminados durante la importación en bloque &#40;SQL Server&#41;](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md).  
  
 Valor de KILOBYTES_PER_BATCH  **=**  *kilobytes_per_batch*  
 Especifica el número aproximado de kilobytes (KB) de datos por lote como *kilobytes_per_batch*. De forma predeterminada, el valor de KILOBYTES_PER_BATCH es desconocido. Para obtener información acerca de consideraciones de rendimiento, vea la sección "Comentarios" más adelante en este tema.  
  
 LASTROW**=***last_row*  
 Especifica el número de la última fila que va a cargarse. El valor predeterminado es 0, que indica la última fila del archivo de datos especificado.  
  
 MAXERRORS  **=**  *max_errors*  
 Especifica el número máximo de errores de sintaxis permitidos en los datos antes de cancelar la operación de importación masiva. Cada fila que no se puede importar con la operación de importación masiva se omite y se considera un error. Si *max_errors* no se especifica, el valor predeterminado es 10.  
  
> [!NOTE]  
>  La opción MAX_ERRORS no se aplica a las comprobaciones de restricción o a la conversión **dinero** y **bigint** tipos de datos.  
  
 ORDEN ({ *columna* [ASC | DESC]} [ **,**... *n* ] )  
 Especifica la forma en que están ordenados los datos del archivo de datos. El rendimiento de la importación masiva mejora si los datos importados se ordenan según el índice clúster de la tabla, si lo hay. Si el archivo de datos se ordenan en un orden diferente, que no sea el orden de una clave de índice agrupado o si no hay ningún índice agrupado en la tabla, se omite la cláusula ORDER. Los nombres de columna facilitados deben ser nombres válidos en la tabla de destino. De forma predeterminada, la operación de inserción masiva presupone que los datos del archivo no están ordenados. En las importaciones masivas optimizadas, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] también valida que los datos importados estén ordenados.  
  
 *n*  
 Es un marcador de posición que indica que se pueden especificar varias columnas.  
  
 ROWS_PER_BATCH  **=**  *rows_per_batch*  
 Indica el número aproximado de filas de datos del archivo de datos.  
  
 De forma predeterminada, todos los datos del archivo de datos se envían al servidor en una sola transacción y el optimizador de consultas desconoce el número de filas del lote. Si especifica ROWS_PER_BATCH (con el valor > 0) el servidor utiliza este valor para optimizar la operación de importación masiva. El valor especificado para ROWS_PER_BATCH debe ser aproximadamente el mismo que el número real de filas. Para obtener información acerca de consideraciones de rendimiento, vea la sección "Comentarios" más adelante en este tema.  
  
 
 TABLOCK  
 Especifica que se obtiene un bloqueo de tabla durante la operación de importación masiva. Varios clientes pueden cargar una tabla simultáneamente si ésta no tiene índices y se especifica TABLOCK. De forma predeterminada, el comportamiento del bloqueo viene determinado por la opción de tabla **table lock on bulk load**. Al mantener un bloqueo durante la operación de importación masiva, se reduce la contención por bloqueos de la tabla y en algunos casos puede mejorarse notablemente el rendimiento. Para obtener información acerca de consideraciones de rendimiento, vea la sección "Comentarios" más adelante en este tema.  
  
 En el índice de almacén de columnas. el comportamiento de bloqueo es diferente porque internamente se divide en varios conjuntos de filas.  Cada subproceso carga datos exclusivamente en cada conjunto de filas aplicando un bloqueo X en el conjunto de filas que permite cargar datos en paralelo con las sesiones de carga de datos simultáneas. El uso de la opción TABLOCK hará que el subproceso realizar un bloqueo X en la tabla (a diferencia de bloqueo de actualización masiva para conjuntos de filas tradicionales) que impedirá que otros subprocesos simultáneos para cargar datos al mismo tiempo.  

### <a name="input-file-format-options"></a>Opciones de formato de archivo de entrada
  
FORMATO  **=**  'CSV'   
**Se aplica a:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
Especifica un archivo de valores separados por comas conforme a la [RFC 4180](https://tools.ietf.org/html/rfc4180) estándar.

FIELDQUOTE  **=**  'field_quote'   
**Se aplica a:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
Especifica un carácter que se usará como el carácter de comillas en el archivo CSV. Si no se especifica, se utilizará el carácter de comillas (") como el carácter de comilla como se define en el [RFC 4180](https://tools.ietf.org/html/rfc4180) estándar.
  
 FORMATFILE **='***format_file_path***'**  
 Especifica la ruta de acceso completa de un archivo de formato. Un archivo de formato describe el archivo de datos que contiene respuestas almacenadas creado mediante el uso de la **bcp** utilidad en la misma tabla o vista. Se debe usar el archivo de formato si:  
  
-   El archivo de datos contiene un número de columnas mayor o menor que la tabla o vista.  
  
-   Las columnas están en un orden diferente.  
  
-   Los delimitadores de columna varían.  
  
-   Hay otros cambios en el formato de los datos. Archivos de formato se crean normalmente mediante la **bcp** utilidad y se modifican con un editor de texto según sea necesario. Para obtener más información, consulte [bcp Utility](../../tools/bcp-utility.md).  

**Se aplica a:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.   
A partir de [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 1.1 CTP, la format_file_path puede estar en el almacenamiento de blobs de Azure.

 FIELDTERMINATOR **='***field_terminator***'**  
 Especifica el terminador de campo que se usará para **char** y **widechar** archivos de datos. El terminador de campo predeterminado es \t (tabulador). Para obtener más información, vea [Especificar terminadores de campo y de fila &#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md).  

 ROWTERMINATOR **='***row_terminator***'**  
 Especifica el terminador de fila que se usará para **char** y **widechar** archivos de datos. El terminador de fila predeterminado es **\r\n** (carácter de nueva línea).  Para obtener más información, vea [Especificar terminadores de campo y de fila &#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md).  

  
## <a name="compatibility"></a>Compatibilidad  
 BULK INSERT aplica una estricta validación y comprobación de los datos leídos de un archivo que pueden dar lugar a errores en los scripts existentes cuando se ejecutan en datos no válidos. Por ejemplo, BULK INSERT comprueba que:  
  
-   Las representaciones nativas de **float** o **real** tipos de datos son válidos.  
  
-   Los datos Unicode tienen una longitud de bytes uniforme.  
  
## <a name="data-types"></a>Tipos de datos  
  
### <a name="string-to-decimal-data-type-conversions"></a>Conversiones de tipos de datos de cadena a decimal  
 Las conversiones de tipos de datos de cadena a decimal utilizadas en BULK INSERT siguen las mismas reglas que la [!INCLUDE[tsql](../../includes/tsql-md.md)] [convertir](../../t-sql/functions/cast-and-convert-transact-sql.md) función, que rechaza las cadenas que representan valores numéricos con notación científica. Por lo tanto, BULK INSERT trata esas cadenas como valores no válidos y genera errores de conversión.  
  
 Para solucionar este comportamiento, use un archivo de formato para la notación científica importar de forma masiva **float** datos en una columna decimal. En el archivo de formato, describa explícitamente la columna como **real** o **float** datos. Para obtener más información acerca de estos tipos de datos, vea [float y real &#40; Transact-SQL &#41; ](../../t-sql/data-types/float-and-real-transact-sql.md).  
  
> [!NOTE]  
>  Archivos de formato representan **real** datos como el **SQLFLT4** tipo de datos y **float** datos como el **SQLFLT8** tipo de datos. Para obtener información acerca de los archivos de formato no XML, vea [especificar tipo de almacenamiento de archivo mediante bcp &#40; SQL Server &#41; ](../../relational-databases/import-export/specify-file-storage-type-by-using-bcp-sql-server.md).  
  
#### <a name="example-of-importing-a-numeric-value-that-uses-scientific-notation"></a>Ejemplo de importación de un valor numérico que utiliza notación científica  
 En este ejemplo se utiliza la siguiente tabla:  
  
```  
CREATE TABLE t_float(c1 float, c2 decimal (5,4));  
```  
  
 El usuario desea importar masivamente datos en la tabla `t_float`. El archivo de datos, C:\t_float-c.dat contiene notación científica **float** datos; por ejemplo:  
  
```  
8.0000000000000002E-28.0000000000000002E-2  
```  
  
 No obstante, BULK INSERT no puede importar estos datos directamente en `t_float`, ya que su segunda columna, `c2`, utiliza el tipo de datos `decimal`. Por lo tanto, es necesario un archivo de formato. El archivo de formato debe asignar la notación científica **float** datos a formato decimal de la columna `c2`.  
  
 El siguiente archivo de formato utiliza el tipo de datos `SQLFLT8` para asignar el segundo campo de datos a la segunda columna:  
  
 ```
 <?xml version="1.0"?> 
 <BCPFORMAT xmlns="http://schemas.microsoft.com/sqlserver/2004/bulkload/format" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"> 
 <RECORD> 
 <FIELD ID="1" xsi:type="CharTerm" TERMINATOR="\t" MAX_LENGTH="30"/> 
 <FIELD ID="2" xsi:type="CharTerm" TERMINATOR="\r\n" MAX_LENGTH="30"/>  </RECORD>  <ROW> 
 <COLUMN SOURCE="1" NAME="c1" xsi:type="SQLFLT8"/> 
 <COLUMN SOURCE="2" NAME="c2" xsi:type="SQLFLT8"/>  </ROW> </BCPFORMAT> 
 ```
  
 Para utilizar este archivo de formato (con el nombre de archivo `C:\t_floatformat-c-xml.xml`) para importar los datos de prueba en la tabla de prueba, emita la siguiente instrucción de [!INCLUDE[tsql](../../includes/tsql-md.md)]:  
  
```  
BULK INSERT bulktest..t_float  
FROM 'C:\t_float-c.dat' WITH (FORMATFILE='C:\t_floatformat-c-xml.xml');  
GO  
```  
  
### <a name="data-types-for-bulk-exporting-or-importing-sqlxml-documents"></a>Tipos de datos para importar o exportar masivamente documentos SQLXML  
 Para importar o exportar de forma masiva datos SQLXML, utilice uno de los tipos de datos siguientes en el archivo de formato:  
  
|Tipo de datos|Efecto|  
|---------------|------------|  
|SQLCHAR o SQLVARCHAR|Los datos se envían a la página de códigos del cliente o a la página de códigos implícita por la intercalación. El efecto es el mismo que si se especifica DATAFILETYPE **= 'char'** sin especificar un archivo de formato.|  
|SQLNCHAR o SQLNVARCHAR|Los datos se envían como datos Unicode. El efecto es el mismo que si se especifica DATAFILETYPE **= 'widechar'** sin especificar un archivo de formato.|  
|SQLBINARY o SQLVARBIN|Los datos se envían sin realizar ninguna conversión.|  
  
## <a name="general-remarks"></a>Notas generales  
 Para obtener una comparación de la instrucción BULK INSERT, la instrucción INSERT ... Seleccione \* instrucción de OPENROWSET y el **bcp** command, consulte [importación en bloque y exportar datos &#40; SQL Server &#41; ](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md).  
  
 Para obtener información sobre cómo preparar datos para la importación masiva, vea [preparar los datos para la exportación masiva o importar &#40; SQL Server &#41; ](../../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md).  
  
 La instrucción BULK INSERT se puede ejecutar en una transacción definida por el usuario para importar datos en una tabla o una vista. Opcionalmente, para utilizar varias coincidencias para la importación masiva de datos, una transacción puede especificar la cláusula BATCHSIZE en la instrucción BULK INSERT. Si una transacción de varios lotes se revierte, cada lote que la transacción ha enviado a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se revierte.  
  
## <a name="interoperability"></a>Interoperabilidad  
  
### <a name="importing-data-from-a-csv-file"></a>Importar datos desde un archivo CSV  
A partir de [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 1.1 CTP, BULK INSERT es compatible con el formato CSV.  
Antes de [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 1.1 CTP, archivos de valores separados por comas (CSV) no son compatibles con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] operaciones de importación masiva. Sin embargo, en algunos casos se puede utilizar un archivo de valores separados por comas (CSV) como archivo de datos para una importación masiva de datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener información acerca de los requisitos para la importación de datos desde un archivo de datos CSV, consulte [preparar los datos para la exportación masiva o importar &#40; SQL Server &#41; ](../../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md).  
  
## <a name="logging-behavior"></a>Comportamiento del registro  
 Para obtener más información sobre cuándo se incluyen en el registro de transacciones las operaciones de inserción de filas que se efectúan durante una importación en bloque, vea [Requisitos previos para el registro mínimo durante la importación en bloque](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md).  
  
##  <a name="Limitations"></a> Restricciones  
 Cuando se usa un archivo de formato con BULK INSERT, solo se puede especificar un máximo de 1024 campos. Es el mismo número máximo de columnas permitido en una tabla. Si usa BULK INSERT con un archivo de datos que contenga más de 1024 campos, BULK INSERT genera el error 4822. El [utilidad bcp](../../tools/bcp-utility.md) no tienen esta limitación, por lo que para los archivos de datos que contienen más de 1024 campos, use la **bcp** comando.  
  
## <a name="performance-considerations"></a>Consideraciones de rendimiento  
 Si el número de páginas que van a vaciarse en un único lote supera un umbral interno, podría producirse un examen completo del grupo de búferes para identificar qué páginas se han de vaciar cuando el lote se confirme. Este examen completo puede afectar de forma desfavorable al rendimiento de la importación masiva. Un caso en el que es probable que se supere el umbral interno se produce cuando un grupo de búferes grande se combina con un subsistema de E/S lento. Para evitar los desbordamientos del búfer en equipos grandes, no utilice la sugerencia TABLOCK (que quita la optimización masiva) o use un tamaño de lote menor (que la preserva).  
  
 Dado que los equipos varían, es recomendable que pruebe varios tamaños de lote con la carga de datos para averiguar lo que funciona mejor en su caso.  
  
## <a name="security"></a>Seguridad  
  
### <a name="security-account-delegation-impersonation"></a>Delegación de cuentas de seguridad (suplantación)  
 Si un usuario utiliza un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , se utilizará el perfil de seguridad de la cuenta de proceso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Un inicio de sesión que use autenticación de SQL Server no se puede autenticar fuera del Motor de base de datos. Por tanto, cuando un inicio de sesión que usa autenticación de SQL Server inicia un comando BULK INSERT, la conexión con los datos se realiza usando el contexto de seguridad de la cuenta de proceso de SQL Server (la cuenta usada por el servicio Motor de base de datos de SQL Server). Para leer correctamente los datos de origen, debe conceder acceso a los datos de origen a la cuenta usada por el Motor de base de datos de SQL Server. Por el contrario, si un usuario de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicia sesión con autenticación de Windows, el usuario solo puede leer aquellos archivos a los que tenga acceso la cuenta de usuario, cualquiera que sea el perfil de seguridad del proceso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Al ejecutar la instrucción BULK INSERT usando **sqlcmd** o **osql**, desde un equipo, insertar datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en un segundo equipo y especificando un *data_file* en tercer equipo mediante el uso de una ruta de acceso UNC, recibirá el error 4861.  
  
 Para resolver este error, use [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación y especificar un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicio de sesión que usa el perfil de seguridad de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuenta de proceso, o bien configure Windows para habilitar la delegación de cuentas de seguridad. Para obtener información acerca de cómo habilitar una cuenta de usuario para que sea de confianza para la delegación, vea la Ayuda de Windows.  
  
 Para obtener más información acerca de ésta y otras consideraciones de seguridad para el uso de BULK INSERT, vea [importación masiva de datos mediante el uso de BULK INSERT u OPENROWSET &#40; BULK... &#41; &#40; SQL Server &#41; ](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md).  
  
### <a name="permissions"></a>Permissions  
 Se requieren los permisos INSERT y ADMINISTER BULK OPERATIONS. Además, es necesario el permiso ALTER TABLE si se da una o varias de las siguientes circunstancias:  
  
-   Existen restricciones y no se ha especificado la opción CHECK_CONSTRAINTS.  
  
    > [!NOTE]  
    >  La deshabilitación de restricciones es el comportamiento predeterminado. Para comprobar las restricciones CHECK explícitamente, utilice la opción CHECK_CONSTRAINTS.  
  
-   Existen desencadenadores y no se ha especificado la opción FIRE_TRIGGER.  
  
    > [!NOTE]  
    >  De forma predeterminada, los desencadenadores no se activan. Para activar los desencadenadores explícitamente, use la opción FIRE_TRIGGER.  
  
-   Se utiliza la opción KEEPIDENTITY para importar el valor de identidad de un archivo de datos.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-pipes-to-import-data-from-a-file"></a>A. Usar canalizaciones para importar datos de un archivo  
 En el siguiente ejemplo se importa información detallada de pedidos en la tabla `AdventureWorks2012.Sales.SalesOrderDetail` desde un archivo de datos especificado utilizando una canalización (`|`) como el terminador de campo y `|\n` como el terminador de fila.  
  
```  
BULK INSERT AdventureWorks2012.Sales.SalesOrderDetail  
   FROM 'f:\orders\lineitem.tbl'  
   WITH   
      (  
         FIELDTERMINATOR =' |',  
         ROWTERMINATOR =' |\n'  
      );  
```  
  
### <a name="b-using-the-firetriggers-argument"></a>B. Usar el argumento FIRE_TRIGGERS  
 En el ejemplo siguiente se especifica el argumento `FIRE_TRIGGERS`.  
  
```  
BULK INSERT AdventureWorks2012.Sales.SalesOrderDetail  
   FROM 'f:\orders\lineitem.tbl'  
   WITH  
     (  
        FIELDTERMINATOR =' |',  
        ROWTERMINATOR = ':\n',  
        FIRE_TRIGGERS  
      );  
```  
  
### <a name="c-using-line-feed-as-a-row-terminator"></a>C. Usar el salto de línea como terminador de fila  
 En el siguiente ejemplo se importa un archivo que utiliza el salto de línea como terminador de fila, igual que en una salida de UNIX:  
  
```  
DECLARE @bulk_cmd varchar(1000);  
SET @bulk_cmd = 'BULK INSERT AdventureWorks2012.Sales.SalesOrderDetail  
FROM ''<drive>:\<path>\<filename>''   
WITH (ROWTERMINATOR = '''+CHAR(10)+''')';  
EXEC(@bulk_cmd);  
```  
  
> [!NOTE]  
>  Debido a la forma en que Microsoft Windows trata los archivos de texto **(\n** automáticamente se reemplaza por **\r\n)**.  
  
### <a name="d-specifying-a-code-page"></a>D. Especificar una página de códigos  
 En el ejemplo siguiente se muestra cómo especificar una página de códigos.  
  
```  
BULK INSERT MyTable  
FROM 'D:\data.csv'  
WITH  
( CODEPAGE = '65001',  
    DATAFILETYPE = 'char',  
    FIELDTERMINATOR = ','  
);  
```  
### <a name="e-importing-data-from-a-csv-file"></a>E. Importar datos desde un archivo CSV   
En el ejemplo siguiente se muestra cómo especificar un archivo CSV.   
```
BULK INSERT Sales.Invoices
FROM '\\share\invoices\inv-2016-07-25.csv'
WITH (FORMAT = 'CSV'); 
```

### <a name="f-importing-data-from-a-file-in-azure-blob-storage"></a>F. Importar datos desde un archivo en el almacenamiento de blobs de Azure   
En el ejemplo siguiente se muestra cómo cargar datos desde un archivo csv en una ubicación de almacenamiento de blobs de Azure, que se ha configurado como origen de datos externo. Esto requiere una credencial de ámbito de la base de datos mediante una firma de acceso compartido.    

```tsql
BULK INSERT Sales.Invoices
FROM 'inv-2017-01-19.csv'
WITH (DATA_SOURCE = 'MyAzureInvoices',
     FORMAT = 'CSV'); 
```

Para completar `BULK INSERT` ejemplos, incluida la configuración de la credencial y el origen de datos externo, vea [ejemplos de forma masiva acceso a los datos en almacenamiento de blobs de Azure](../../relational-databases/import-export/examples-of-bulk-access-to-data-in-azure-blob-storage.md).
  
### <a name="additional-examples"></a>Otros ejemplos  
 Otros `BULK INSERT` se proporcionan ejemplos en los temas siguientes:  
  
-   [Ejemplos de importación y exportación en bloque de documentos XML &#40;SQL Server&#41;](../../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)  
  
-   [Mantener valores de identidad al importar datos en bloque &#40;SQL Server&#41;](../../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md)  
  
-   [Mantener valores NULL o usar valores predeterminados durante la importación en bloque &#40;SQL Server&#41;](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)  
  
-   [Especificar terminadores de campo y de fila &#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)  
  
-   [Usar un archivo de formato para importar datos en bloque &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)  
  
-   [Usar el formato de caracteres para importar o exportar datos &#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar el formato nativo para importar o exportar datos &#40;SQL Server&#41;](../../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar el formato de caracteres Unicode para importar o exportar datos &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar el formato nativo Unicode para importar o exportar datos &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar un archivo de formato para omitir una columna de tabla &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
-   [Usar un archivo de formato para asignar columnas de tabla a campos de un archivo de datos &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
## <a name="see-also"></a>Vea también  
 [Importar y exportar datos en bloque &#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)   
 [bcp Utility](../../tools/bcp-utility.md)   
 [Archivos de formato para importar o exportar datos &#40; SQL Server &#41;](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [Preparar los datos para la exportación o importación &#40; SQL Server &#41;](../../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md)   
 [sp_tableoption &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md)  
  
  
