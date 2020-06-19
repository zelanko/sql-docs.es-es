---
title: Mantenimiento de valores NULL o uso de valores predeterminados durante la importación en bloque (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- bulk importing [SQL Server], null values
- bulk importing [SQL Server], default values
- data formats [SQL Server], null values
- bulk rowset providers [SQL Server]
- bcp utility [SQL Server], null values
- BULK INSERT statement
- default values
- OPENROWSET function, bulk importing
- data formats [SQL Server], default values
ms.assetid: 6b91d762-337b-4345-a159-88abb3e64a81
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 856aa12f6ad5e5094324e0df65941bc63d611451
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85026689"
---
# <a name="keep-nulls-or-use-default-values-during-bulk-import-sql-server"></a>Mantener valores NULL o usar valores predeterminados durante la importación masiva (SQL Server)
  De manera predeterminada, cuando se importan datos en una tabla, el comando **BCP** y la instrucción BULK INSERT aplican los valores predeterminados definidos para las columnas de la tabla. Por ejemplo, si un archivo de datos contiene un campo NULL, en su lugar, se cargará el valor predeterminado para la columna. El comando **BCP** y la instrucción BULK INSERT permiten especificar que se mantengan los valores NULL.  
  
 Por el contrario, una instrucción INSERT normal mantiene el valor NULL en lugar de insertar un valor predeterminado. La instrucción INSERT ... La instrucción SELECT * FROM OPENROWSET(BULK...) proporciona el mismo comportamiento básico que la instrucción INSERT regular, pero además admite una sugerencia de tabla para insertar los valores predeterminados.  
  
> [!NOTE]  
>  En los archivos de formato de ejemplo que omiten una columna de tabla, vea [Usar un archivo de formato para omitir una columna de tabla &#40;SQL Server&#41;](use-a-format-file-to-skip-a-table-column-sql-server.md).  
  
## <a name="sample-table-and-data-file"></a>Tabla y archivo de datos de ejemplo  
 Para ejecutar los ejemplos de este tema, es necesario crear una tabla y un archivo de datos de ejemplo.  
  
### <a name="sample-table"></a>Tabla de ejemplo  
 Los ejemplos requieren la creación de una tabla denominada **MyTestDefaultCol2** en la base de datos de ejemplo **AdventureWorks** , bajo el esquema **dbo** . Para crear esta tabla, en el [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] Editor de consultas, ejecute:  
  
```  
USE AdventureWorks;  
GO  
CREATE TABLE MyTestDefaultCol2   
(Col1 smallint,  
Col2 nvarchar(50) DEFAULT 'Default value of Col2',  
Col3 nvarchar(50)   
);  
GO  
  
```  
  
 Tenga en cuenta que la segunda columna de la tabla, `Col2`, tiene un valor predeterminado.  
  
### <a name="sample-format-file"></a>Archivo de formato de ejemplo  
 Algunos de los ejemplos de importación masiva utilizan un archivo de formato no XML, `MyTestDefaultCol2-f-c.Fmt`, que corresponde exactamente a la tabla `MyTestDefaultCol2`. Para crear este archivo de formato, en el símbolo del sistema de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows, especifique:  
  
```  
bcp AdventureWorks..MyTestDefaultCol2 format nul -c -f C:\MyTestDefaultCol2-f-c.Fmt -t, -r\n -T  
  
```  
  
 Para obtener más información sobre cómo crear archivos de formato, vea [Crear un archivo de formato &#40;SQL Server&#41;](create-a-format-file-sql-server.md).  
  
### <a name="sample-data-file"></a>Archivo de datos de ejemplo  
 El ejemplo utiliza un archivo de datos de ejemplo, `MyTestEmptyField2-c.Dat`, que no contiene valores en el segundo campo. El archivo de datos `MyTestEmptyField2-c.Dat` contiene los siguientes registros.  
  
```  
1,,DataField3  
2,,DataField3  
  
```  
  
## <a name="keeping-null-values-with-bcp-or-bulk-insert"></a>Mantener valores NULL con bcp o BULK INSERT  
 Los siguientes calificadores especifican que un campo vacío del archivo de datos mantiene su valor NULL durante la operación de importación masiva, en lugar de heredar un valor predeterminado (si existe) para las columnas de la tabla.  
  
|Get-Help|Qualifier|Tipo de calificador|  
|-------------|---------------|--------------------|  
|**bcp**|`-k`|Switch|  
|BULK INSERT|KEEPNULLS<sup>1</sup>|Argumento|  
  
 <sup>1</sup> para Bulk Insert, si los valores predeterminados no están disponibles, se debe definir la columna de la tabla para permitir valores NULL.  
  
> [!NOTE]  
>  Estos calificadores deshabilitan la comprobación de definiciones DEFAULT en una tabla mediante los comandos de importación masiva. Sin embargo, para cualquier instrucción INSERT simultánea, se esperan definiciones DEFAULT.  
  
 Para obtener más información, vea [bcp (utilidad)](../../tools/bcp-utility.md) y [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql).  
  
### <a name="examples"></a>Ejemplos  
 Los ejemplos de esta sección realizan importaciones masivas mediante **bcp** o BULK INSERT y mantienen los valores NULL.  
  
 La segunda columna de la tabla, **Col2**, tiene un valor predeterminado. El campo correspondiente del archivo de datos contiene una cadena vacía. De forma predeterminada, cuando se usa **bcp** o BULK INSERT para importar datos de este archivo de datos en la tabla **MyTestDefaultCol2** , se inserta el valor predeterminado de **Col2** , obteniéndose el siguiente resultado:  
  
||||  
|-|-|-|  
|`1`|`Default value of Col2`|`DataField3`|  
|`2`|`Default value of Col2`|`DataField3`|  
  
 Para insertar " `NULL` " en lugar de " `Default value of Col2` ", debe usar la `-k` opción switch o KEEPNULL, tal y como se muestra en los siguientes ejemplos de **BCP** y Bulk Insert.  
  
#### <a name="using-bcp-and-keeping-null-values"></a>Usar bcp y mantener valores NULL  
 En el siguiente ejemplo se muestra cómo mantener valores NULL en un comando **bcp** . El comando **BCP** contiene los siguientes modificadores:  
  
|Modificador|Descripción|  
|------------|-----------------|  
|`-f`|Especifica que el comando utiliza un archivo de formato.|  
|`-k`|Especifica que las columnas vacías deben conservar un valor NULL durante la operación, en vez de tener valores predeterminados para las columnas insertadas.|  
|`-T`|Especifica que la utilidad bcp se conecte a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante una conexión de confianza.|  
  
 En el símbolo del sistema de Windows, escriba:  
  
```  
bcp AdventureWorks..MyTestDefaultCol2 in C:\MyTestEmptyField2-c.Dat -f C:\MyTestDefaultCol2-f-c.Fmt -k -T  
  
```  
  
#### <a name="using-bulk-insert-and-keeping-null-values"></a>Usar BULK INSERT y mantener valores NULL  
 En el siguiente ejemplo se muestra el uso de la opción KEEPNULLS en una instrucción BULK INSERT. En una herramienta de consulta, como el Editor de consultas de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], ejecute:  
  
```  
USE AdventureWorks;  
GO  
BULK INSERT MyTestDefaultCol2  
   FROM 'C:\MyTestEmptyField2-c.Dat'  
   WITH (  
      DATAFILETYPE = 'char',  
      FIELDTERMINATOR = ',',  
      KEEPNULLS  
   );  
GO  
  
```  
  
## <a name="keeping-default-values-with-insert--select--from-openrowsetbulk"></a>Manteniendo los valores predeterminados con INSERT... SELECT * FROM OPENROWSET (BULK...)  
 De forma predeterminada, las columnas que no se especifican en la operación de carga masiva se establecen en NULL mediante INSERT... SELECT * FROM OPENROWSET (BULK...). Sin embargo, puede especificar que para un campo vacío del archivo de datos, la columna de la tabla correspondiente utilice su valor predeterminado (si existe). Para usar los valores predeterminados, especifique la siguiente sugerencia de tabla:  
  
|Get-Help|Qualifier|Tipo de calificador|  
|-------------|---------------|--------------------|  
|INSERT ... SELECT * FROM OPENROWSET(BULK...)|WITH(KEEPDEFAULTS)|Sugerencia de tabla|  
  
> [!NOTE]  
>  para obtener más información, vea [INSERT &#40;Transact-sql&#41;](/sql/t-sql/statements/insert-transact-sql), [Select &#40;transact-SQL&#41;](/sql/t-sql/queries/select-transact-sql), [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)y [sugerencias de tabla &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-table)  
  
### <a name="examples"></a>Ejemplos  
 La siguiente instrucción INSERT... El ejemplo SELECT * FROM OPENROWSET (BULK...) realiza importaciones masivas de datos y mantiene los valores predeterminados.  
  
 Para ejecutar los ejemplos es necesario crear la tabla de ejemplo **MyTestDefaultCol2** y el archivo de datos `MyTestEmptyField2-c.Dat` y usar un archivo de formato, `MyTestDefaultCol2-f-c.Fmt`. Para obtener más información acerca de la creación de estos ejemplos, vea "Tabla y archivo de datos de ejemplo", más arriba en este tema.  
  
 La segunda columna de la tabla, **Col2**, tiene un valor predeterminado. El campo correspondiente del archivo de datos contiene una cadena vacía. Cuando INSERT... SELECT \* from OPENROWSET (bulk...) importar los campos de este archivo de datos en la tabla **MyTestDefaultCol2** , de forma predeterminada, NULL se inserta en **Col2** en lugar del valor predeterminado. Este comportamiento predeterminado genera el siguiente resultado:  
  
||||  
|-|-|-|  
|`1`|`NULL`|`DataField3`|  
|`2`|`NULL`|`DataField3`|  
  
 Para insertar el valor predeterminado, "`Default value of Col2`", en lugar de "`NULL`", es necesario usar la sugerencia de tabla KEEPDEFAULTS, como se muestra en el siguiente ejemplo. En una herramienta de consulta, como el Editor de consultas de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], ejecute:  
  
```  
USE AdventureWorks;  
GO  
INSERT INTO MyTestDefaultCol2  
    WITH (KEEPDEFAULTS)  
    SELECT *  
      FROM OPENROWSET(BULK  'C:\MyTestEmptyField2-c.Dat',  
      FORMATFILE='C:\MyTestDefaultCol2-f-c.Fmt'       
      ) as t1 ;  
GO  
  
```  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Tareas relacionadas  
  
-   [Mantener valores de identidad al importar datos en bloque &#40;SQL Server&#41;](keep-identity-values-when-bulk-importing-data-sql-server.md)  
  
-   [Preparar los datos para exportar o importar en bloque &#40;SQL Server&#41;](prepare-data-for-bulk-export-or-import-sql-server.md)  
  
 **Para usar un archivo de formato**  
  
-   [Crear un archivo de formato &#40;SQL Server&#41;](create-a-format-file-sql-server.md)  
  
-   [Usar un archivo de formato para importar datos en bloque &#40;SQL Server&#41;](use-a-format-file-to-bulk-import-data-sql-server.md)  
  
-   [Usar un archivo de formato para asignar columnas de tabla a campos de un archivo de datos &#40;SQL Server&#41;](use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
-   [Usar un archivo de formato para omitir un campo de datos &#40;SQL Server&#41;](use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
-   [Usar un archivo de formato para omitir una columna de tabla &#40;SQL Server&#41;](use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
 **Para usar formatos de datos para la importación o exportación masivas**  
  
-   [Importar datos con formato nativo y de caracteres de versiones anteriores de SQL Server](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
-   [Usar el formato de caracteres para importar o exportar datos &#40;SQL Server&#41;](use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar el formato nativo para importar o exportar datos &#40;SQL Server&#41;](use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar el formato de caracteres Unicode para importar o exportar datos &#40;SQL Server&#41;](use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar el formato nativo Unicode para importar o exportar datos &#40;SQL Server&#41;](use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
 **Para especificar formatos de datos por razones de compatibilidad cuando se usa bcp**  
  
-   [Especificar terminadores de campo y de fila &#40;SQL Server&#41;](specify-field-and-row-terminators-sql-server.md)  
  
-   [Especificar la longitud de prefijo en los archivos de datos mediante bcp &#40;SQL Server&#41;](specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)  
  
-   [Especificar el tipo de almacenamiento en archivo mediante bcp &#40;SQL Server&#41;](specify-file-storage-type-by-using-bcp-sql-server.md)  
  
## <a name="see-also"></a>Consulte también  
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [bcp (utilidad)](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [Sugerencias de tabla &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-table)  
  
  
