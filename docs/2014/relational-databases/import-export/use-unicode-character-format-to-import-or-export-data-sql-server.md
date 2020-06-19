---
title: Usar el formato de caracteres Unicode para importar o exportar datos (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- data formats [SQL Server], Unicode character
- Unicode [SQL Server], bulk importing and exporting
ms.assetid: 74342a11-c1c0-4746-b482-7f3537744a70
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 520ce1b4eed8dc11d6d3fe038969257aea1e90fd
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85026361"
---
# <a name="use-unicode-character-format-to-import-or-export-data-sql-server"></a>Usar el formato de caracteres Unicode para importar o exportar datos (SQL Server)
  El formato de caracteres Unicode se recomienda para las transferencias masivas de datos entre varias instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante un archivo de datos que contenga caracteres DBCS o extendidos. El formato de datos de caracteres Unicode permite exportar datos desde un servidor mediante una página de códigos utilizada por el cliente que está realizando la operación. En esos casos, el uso del formato de caracteres Unicode tiene las siguientes ventajas:  
  
-   Si los datos de origen y destino son de tipo Unicode, el uso del formato de caracteres Unicode mantiene todos los datos de los caracteres.  
  
-   Si los datos de origen y destino no son de tipo Unicode, el uso del formato de caracteres Unicode minimiza la pérdida de caracteres extendidos en los datos de origen que no pueden representarse en el destino.  
  
 Los archivos de datos con formato de caracteres Unicode utilizan las convenciones de los archivos Unicode. Los primeros dos bytes del archivo son los números hexadecimales 0xFFFE. Estos bytes funcionan como marcas de orden de bytes, ya que especifican si el byte de orden alto se almacena el primero o el último en el archivo.  
  
> [!IMPORTANT]  
>  Para que un archivo de formato trabaje con un archivo de datos de caracteres Unicode, todos los campos de entrada deben ser cadenas de texto Unicode (es decir, de tamaño fijo o cadenas Unicode terminadas en caracteres).  
  
 Los datos `sql_variant` almacenados en un archivo de datos con formato de caracteres Unicode funcionan de la misma forma que en un archivo de datos en modo de caracteres, con la excepción de que los datos se almacenan como `nchar` en lugar de `char`. Para obtener más información sobre el formato de caracteres, consulte [Compatibilidad con la intercalación y Unicode](../collations/collation-and-unicode-support.md).  
  
 Para usar un terminador de campo o de fila distinto al predeterminado que se proporciona con el formato de caracteres Unicode, vea [Especificar terminadores de campo y de fila &#40;SQL Server&#41;](specify-field-and-row-terminators-sql-server.md).  
  
## <a name="command-options-for-unicode-character-format"></a>Opciones de comando para el formato de caracteres Unicode  
 Puede importar datos con formato de caracteres Unicode en una tabla mediante **BCP**, Bulk Insert o INSERT... SELECT \* from OPENROWSET (bulk...). Para un comando **BCP** o una instrucción BULK INSERT, puede especificar el formato de datos en la línea de comandos. Para una instrucción INSERT ... SELECT * FROM OPENROWSET(BULK...), debe especificar el formato de datos en un archivo de formato.  
  
 El formato de caracteres Unicode puede usarse con las siguientes opciones de la línea de comandos:  
  
|Get-Help|Opción|Description|  
|-------------|------------|-----------------|  
|**bcp**|**-w**|Usa el formato de caracteres Unicode.|  
|BULK INSERT|DATAFILETYPE **= '** WideChar **'**|Utiliza el formato de caracteres Unicode al importar datos masivamente.|  
  
 Para obtener más información, vea [bcp (utilidad)](../../tools/bcp-utility.md), [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql) u [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql).  
  
> [!NOTE]  
>  Otra posibilidad es especificar el formato por campo en un archivo de formato. Para obtener más información, vea [Archivos de formato para importar o exportar datos &#40;SQL Server&#41;](format-files-for-importing-or-exporting-data-sql-server.md).  
  
## <a name="examples"></a>Ejemplos  
 En los siguientes ejemplos se muestra el modo de exportar datos de forma masiva con formato de datos de caracteres Unicode mediante **bcp** e importar masivamente los mismos datos mediante BULK INSERT.  
  
### <a name="sample-table"></a>Tabla de ejemplo  
 Los ejemplos requieren la creación de una tabla denominada `myTestUniCharData` en la base de datos de ejemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] , bajo el esquema `dbo` . Antes de poder ejecutar los ejemplos, debe crear esta tabla. Para crear esta tabla, en el Editor de consultas de [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] , ejecute:  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE myTestUniCharData (  
   Col1 smallint,  
   Col2 nvarchar(50),  
   Col3 nvarchar(50)  
   );   
```  
  
 Para rellenar esta tabla y ver el contenido resultante, ejecute las siguientes instrucciones:  
  
```  
INSERT INTO myTestUniCharData(Col1,Col2,Col3)  
   VALUES(1,'DataField2','DataField3')   
        ,(2,'DataField2','DataField3');  
GO  
SELECT Col1,Col2,Col3 FROM myTestUniCharData;  
  
```  
  
### <a name="using-bcp-to-bulk-export-unicode-character-data"></a>Usar bcp para exportar masivamente datos con formato de datos de caracteres Unicode  
 Para exportar datos de la tabla a un archivo de datos, use **bcp** con la opción **out** y los siguientes calificadores:  
  
|Calificadores|Descripción|  
|----------------|-----------------|  
|**-w**|Especifica el formato de caracteres Unicode.|  
|**-t** `,`|Especifica una coma (`,`) como terminador de campo.<br /><br /> Nota: el terminador de campo predeterminado es el carácter Unicode de tabulación (\t). Para obtener más información, vea [Especificar terminadores de campo y de fila &#40;SQL Server&#41;](specify-field-and-row-terminators-sql-server.md).|  
|**-T**|Especifica que la utilidad **bcp** se conecta a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con una conexión de confianza utilizando la seguridad integrada. Si no se especifica **-T** , es necesario especificar **-U** y **-P** para iniciar sesión correctamente.|  
  
 En el siguiente ejemplo se exportan masivamente datos en formato de caracteres Unicode desde la tabla `myTestUniCharData` en un nuevo archivo de datos denominado `myTestUniCharData-w.Dat` que usa la coma (`,`) como terminador de campo. En el símbolo del sistema de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows, especifique:  
  
```  
bcp AdventureWorks2012..myTestUniCharData out C:\myTestUniCharData-w.Dat -w -t, -T  
  
```  
  
### <a name="using-bulk-insert-to-bulk-import-unicode-character-data"></a>Usar BULK INSERT para importar masivamente datos con formato de caracteres Unicode  
 En el siguiente ejemplo se utiliza `BULK INSERT` para importar los datos del archivo de datos `myTestUniCharData-w.Dat` a la tabla `myTestUniCharData`. Es necesario declarar en la instrucción el terminador de campo no predeterminado (`,`). En el Editor de consultas de [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], ejecute:  
  
```  
USE AdventureWorks2012;  
GO  
BULK INSERT myTestUniCharData   
   FROM 'C:\myTestUniCharData-w.Dat'   
   WITH (  
      DATAFILETYPE='widechar',  
      FIELDTERMINATOR=','  
   );   
GO  
SELECT Col1,Col2,Col3 FROM myTestUniCharData;  
GO  
  
```  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Tareas relacionadas  
 **Para usar formatos de datos para la importación o exportación masivas**  
  
-   [Importar datos con formato nativo y de caracteres de versiones anteriores de SQL Server](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
-   [Usar el formato de caracteres para importar o exportar datos &#40;SQL Server&#41;](use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar el formato nativo para importar o exportar datos &#40;SQL Server&#41;](use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar el formato nativo Unicode para importar o exportar datos &#40;SQL Server&#41;](use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
## <a name="see-also"></a>Consulte también  
 [bcp (utilidad)](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [Tipos de datos &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql)   
 [Compatibilidad con la intercalación y Unicode](../collations/collation-and-unicode-support.md)  
  
  
