---
title: Mantenimiento de valores de identidad al importar datos de forma masiva (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- identity values [SQL Server], bulk imports
- data formats [SQL Server], identity values
- bulk importing [SQL Server], identity values
ms.assetid: 45894a3f-2d8a-4edd-9568-afa7d0d3061f
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c994a04f41b548599deff4ff5a0a99ba89be6c7f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63064591"
---
# <a name="keep-identity-values-when-bulk-importing-data-sql-server"></a>Mantener valores de identidad al importar datos de forma masiva (SQL Server)
  Los archivos de datos contienen valores de identidad que pueden importarse de forma masiva en una instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. De manera predeterminada, los valores de la columna de identidad del archivo de datos que se importa se omiten y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] asigna automáticamente valores únicos. Los valores únicos se basan en los valores de inicialización y de incremento especificados durante la creación de la tabla.  
  
 Si el archivo de datos no contiene valores para la columna de identificadores de la tabla, use el archivo de formato para especificar que se debe omitir esta columna al importar los datos. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] asignará automáticamente valores exclusivos para la columna.  
  
 Para impedir que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] asigne valores de identidad al importar de forma masiva filas de datos en una tabla, utilice el calificador de comando adecuado para mantener la identidad. Al especificar un calificador para mantener la identidad, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza los valores de identidad del archivo de datos. Estos calificadores son:  
  
|Comando|Calificador para mantener la identidad|Tipo de calificador|  
|-------------|------------------------------|--------------------|  
|`bcp`|**-E**|Modificador|  
|BULK INSERT|KEEPIDENTITY|Argumento|  
|INSERT ... SELECT * FROM OPENROWSET(BULK...)|KEEPIDENTITY|Sugerencia de tabla|  
  
 Para obtener más información, vea [bcp (utilidad)](../../tools/bcp-utility.md), [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql), [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql), [INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/insert-transact-sql), [SELECT &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-transact-sql) y [Sugerencias de tabla &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-table).  
  
> [!NOTE]  
>  Para crear un número que se incremente automáticamente y que se pueda usar en varias tablas, o que se pueda llamar desde las aplicaciones sin hacer referencia a ninguna tabla, vea [Números de secuencia](../sequence-numbers/sequence-numbers.md).  
  
## <a name="examples"></a>Ejemplos  
 En los ejemplos de este tema se realiza una importación masiva de datos utilizando INSERT ... SELECT * FROM OPENROWSET(BULK...) y se mantienen los valores predeterminados.  
  
### <a name="sample-table"></a>Tabla de ejemplo  
 En ejemplos de importación en bloque, es necesario crear una tabla denominada **myTestKeepNulls** en la base de datos de ejemplo **AdventureWorks** en el esquema **dbo**. Para crear esta tabla en el Editor de consultas de [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], ejecute:  
  
```  
USE AdventureWorks;  
GO  
SELECT * INTO HumanResources.myDepartment   
   FROM HumanResources.Department  
      WHERE 1=0;  
GO  
SELECT * FROM HumanResources.myDepartment;  
```  
  
 La tabla **Department** en la que se basa `myDepartment` tiene IDENTITY_INSERT establecido en OFF. Por tanto, para importar datos en una columna de identidad, debe especificar KEEPIDENTITY o **-E**.  
  
### <a name="sample-data-file"></a>Archivo de datos de ejemplo  
 El archivo de datos usado en los ejemplos de importación masiva contiene datos exportados de forma masiva desde la tabla `HumanResources.Department` en formato nativo. Para crear el archivo de datos, en el símbolo del sistema de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows, escriba:  
  
```  
bcp AdventureWorks.HumanResources.Department out myDepartment-n.Dat -n -T  
```  
  
### <a name="sample-format-file"></a>Archivo de formato de ejemplo  
 En este ejemplo de importación masiva se usa un archivo de formato XML, `myDepartment-f-x-n.Xml`, que usa formatos de datos nativos. En este ejemplo se usa `bcp` para generar este archivo de formato desde la tabla `HumanResources.Department` de la base de datos `AdventureWorks`. En el símbolo del sistema de Windows, escriba:  
  
```  
bcp AdventureWorks.HumanResources.Department format nul -n -x -f myDepartment-f-n-x.Xml -T  
```  
  
 Para obtener más información sobre cómo crear un archivo de formato, vea [Crear un archivo de formato &#40;SQL Server&#41;](create-a-format-file-sql-server.md).  
  
### <a name="a-using-bcp-and-keeping-identity-values"></a>A. Usar bcp y mantener valores de identidad  
 En el siguiente ejemplo se muestra cómo mantener valores de identidad al usar `bcp` para importar datos de forma masiva. El comando `bcp` usa el archivo de formato, `myDepartment-f-n-x.Xml`, y contiene los siguientes modificadores:  
  
|Calificadores|Descripción|  
|----------------|-----------------|  
|**-E**|Especifica el valor o valores de identidad del archivo de datos que se van a usar en la columna de identidad.|  
|**-T**|Especifica que el `bcp` utilidad se conecta a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con una conexión de confianza.|  
  
 En el símbolo del sistema de Windows, escriba:  
  
```  
bcp AdventureWorks.HumanResources.myDepartment in C:\myDepartment-n.Dat -f C:\myDepartment-f-n-x.Xml -E -T  
  
```  
  
### <a name="b-using-bulk-insert-and-keeping-identity-values"></a>b. Usar BULK INSERT y mantener valores de identidad  
 En el siguiente ejemplo se utiliza BULK INSERT para realizar una importación masiva de datos desde el archivo `myDepartment-c.Dat` en la tabla `AdventureWorks.HumanResources.myDepartment` . La instrucción utiliza el archivo de formato `myDepartment-f-n-x.Xml` e incluye la opción KEEPIDENTITY para que se mantengan todos los valores de identidad del archivo de datos.  
  
 En el Editor de consultas de [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], ejecute:  
  
```  
USE AdventureWorks;  
GO  
DELETE HumanResources.myDepartment;  
GO  
BULK INSERT HumanResources.myDepartment  
   FROM 'C:\myDepartment-n.Dat'  
   WITH (  
      KEEPIDENTITY,  
      FORMATFILE='C:\myDepartment-f-n-x.Xml'  
   );  
GO  
SELECT * FROM HumanResources.myDepartment;  
  
```  
  
### <a name="c-using-openrowset-and-keeping-identity-values"></a>C. Usar OPENROWSET y mantener valores de identidad  
 En el siguiente ejemplo se utiliza el proveedor de conjuntos de filas BULK, OPENROWSET, para realizar una importación masiva de datos desde el archivo `myDepartment-c.Dat` en la tabla `AdventureWorks.HumanResources.myDepartment` . La instrucción utiliza el archivo de formato `myDepartment-f-n-x.Xml` e incluye la sugerencia KEEPIDENTITY para que se mantengan todos los valores de identidad del archivo de datos.  
  
 En el Editor de consultas de [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], ejecute:  
  
```  
USE AdventureWorks;  
GO  
DELETE HumanResources.myDepartment;  
GO  
  
INSERT INTO HumanResources.myDepartment  
   with (KEEPIDENTITY)  
   (DepartmentID, Name, GroupName, ModifiedDate)  
   SELECT *  
      FROM  OPENROWSET(BULK 'C:\myDepartment-n.Dat',  
      FORMATFILE='C:\myDepartment-f-n-x.Xml') as t1;  
GO  
  
```  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
  
-   [Mantener valores NULL o usar valores predeterminados durante la importación en bloque &#40;SQL Server&#41;](keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)  
  
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
  
1.  [Especificar terminadores de campo y de fila &#40;SQL Server&#41;](specify-field-and-row-terminators-sql-server.md)  
  
2.  [Especificar la longitud de prefijo en los archivos de datos mediante bcp &#40;SQL Server&#41;](specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)  
  
3.  [Especificar el tipo de almacenamiento en archivo mediante bcp &#40;SQL Server&#41;](specify-file-storage-type-by-using-bcp-sql-server.md)  
  
## <a name="see-also"></a>Vea también  
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [bcp (utilidad)](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [Sugerencias de tabla &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-table)  
  
  
