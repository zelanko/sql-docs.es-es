---
title: Usar el formato nativo Unicode para importar o exportar datos (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- Unicode [SQL Server], bulk importing and exporting
- data formats [SQL Server], Unicode native
ms.assetid: a6213308-f3d5-406e-9029-19d8bb3367f3
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b1d115dacc53cb074080931c2ebad88dcaf1c68d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66011565"
---
# <a name="use-unicode-native-format-to-import-or-export-data-sql-server"></a>Usar el formato nativo Unicode para importar o exportar datos (SQL Server)
  El formato nativo Unicode es útil cuando se debe copiar información de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] una instalación de a otra. El uso del formato nativo para datos que no son caracteres permite ahorrar tiempo, además de evitar la conversión innecesaria de tipos de datos a y desde el formato de caracteres. El uso del formato de caracteres Unicode para todos los datos de caracteres evita la pérdida de caracteres extendidos durante la transferencia masiva de datos entre servidores que utilizan páginas de códigos diferentes. Los archivos de datos en formato nativo Unicode se pueden leer en cualquier método de importación masiva.  
  
 El formato nativo Unicode se recomienda para la transferencia masiva de datos entre varias instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante un archivo de datos que contenga caracteres extendidos o DBCS. Para los datos que no son caracteres, el formato nativo Unicode utiliza tipos de datos nativos (de base de datos). Para los datos de caracteres, como `char`, `nchar`, `varchar`, `nvarchar`, `text`, `varchar(max)`, `nvarchar(max)` y `ntext`, el formato nativo Unicode utiliza el formato de datos de caracteres Unicode.  
  
 Los datos `sql_variant` que se almacenan como SQLVARIANT en un archivo de datos en formato nativo Unicode funcionan de la misma manera que en un archivo de datos en formato nativo, con la excepción de que los valores `char` y `varchar` se convierten en `nchar` y `nvarchar`, lo que duplica la cantidad de espacio necesario para las columnas afectadas. Los metadatos originales se conservan y los valores se convierten de nuevo al tipo de datos `char` y `varchar` original cuando se importan masivamente en la columna de una tabla.  
  
## <a name="command-options-for-unicode-native-format"></a>Opciones de comandos para el formato nativo Unicode  
 Puede importar datos con formato nativo Unicode en una tabla mediante **BCP**, Bulk Insert o INSERT... SELECT \* from OPENROWSET (bulk...). Para un comando **BCP** o una instrucción BULK INSERT, puede especificar el formato de datos en la línea de comandos. Para una instrucción INSERT ... SELECT * FROM OPENROWSET(BULK...) , debe especificar el formato de datos en un archivo de formato.  
  
 El formato nativo Unicode puede usarse con las siguientes opciones:  
  
|Get-Help|Opción|Descripción|  
|-------------|------------|-----------------|  
|**BCP**|**-N**|Hace que la utilidad **BCP** use el formato nativo Unicode, que utiliza tipos de datos nativos (de base de datos) para todos los datos que no son caracteres y el formato`char`de `nchar`datos `varchar`de `nvarchar`caracteres `text`Unicode `ntext`para todos los datos de caracteres (,,,, y).|  
|BULK INSERT|DATAFILETYPE **='** widenative **'**|Utilice el formato nativo Unicode al importar datos masivamente.|  
  
 Para obtener más información, vea [bcp (utilidad)](../../tools/bcp-utility.md), [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql) u [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql).  
  
> [!NOTE]  
>  Otra posibilidad es especificar el formato por campo en un archivo de formato. Para obtener más información, vea [Archivos de formato para importar o exportar datos &#40;SQL Server&#41;](format-files-for-importing-or-exporting-data-sql-server.md).  
  
## <a name="examples"></a>Ejemplos  
 En los siguientes ejemplos se muestra el modo de exportar masivamente datos nativos con **bcp** e importar masivamente los mismos datos mediante BULK INSERT.  
  
### <a name="sample-table"></a>Tabla de ejemplo  
 Los ejemplos requieren que se cree una tabla denominada **myTestUniNativeData** en la base de datos de ejemplo **AdventureWorks** , bajo el esquema **dbo** . Antes de poder ejecutar los ejemplos, debe crear esta tabla. En el Editor de consultas de [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] , ejecute:  
  
```  
USE AdventureWorks;  
GO  
CREATE TABLE myTestUniNativeData (  
   Col1 smallint,  
   Col2 nvarchar(50),  
   Col3 nvarchar(50)  
   );   
```  
  
 Para rellenar esta tabla y ver el contenido resultante, ejecute las siguientes instrucciones:  
  
```  
INSERT INTO myTestUniNativeData(Col1,Col2,Col3)  
   VALUES(1,'DataField2','DataField3');  
INSERT INTO myTestUniNativeData(Col1,Col2,Col3)  
   VALUES(2,'DataField2','DataField3');  
GO  
SELECT Col1,Col2,Col3 FROM myTestUniNativeData  
  
```  
  
### <a name="using-bcp-to-bulk-export-native-data"></a>Usar bcp para exportar masivamente datos nativos  
 Para exportar datos de la tabla a un archivo de datos, use **bcp** con la opción **out** y los siguientes calificadores:  
  
|Calificadores|Descripción|  
|----------------|-----------------|  
|**-N**|Especifica tipos de datos nativos.|  
|**-T**|Especifica que la utilidad **bcp** se conecta a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con una conexión de confianza utilizando la seguridad integrada. Si no se especifica **-T** , es necesario especificar **-U** y **-P** para iniciar sesión correctamente.|  
  
 En el siguiente ejemplo se exportan masivamente datos en formato nativo desde la tabla `myTestUniNativeData` a un nuevo archivo de datos denominado `myTestUniNativeData-N.Dat`. En el símbolo del sistema de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows, especifique:  
  
```  
bcp AdventureWorks..myTestUniNativeData out C:\myTestUniNativeData-N.Dat -N -T  
  
```  
  
### <a name="using-bulk-insert-to-bulk-import-native-data"></a>Usar BULK INSERT para importar masivamente datos nativos  
 En el siguiente ejemplo se utiliza BULK INSERT para importar los datos del archivo de datos `myTestUniNativeData-N.Dat` en la tabla `myTestUniNativeData` . En el Editor de consultas de [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] , ejecute:  
  
```  
USE AdventureWorks;  
GO  
BULK INSERT myTestUniNativeData   
    FROM 'C:\myTestUniNativeData-N.Dat'   
   WITH (DATAFILETYPE='widenative');   
GO  
SELECT Col1,Col2,Col3 FROM myTestUniNativeData;  
GO  
  
```  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
 **Para usar formatos de datos para la importación o exportación masivas**  
  
-   [Importar datos con formato nativo y de caracteres de versiones anteriores de SQL Server](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
-   [Usar el formato de caracteres para importar o exportar datos &#40;SQL Server&#41;](use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar el formato nativo para importar o exportar datos &#40;SQL Server&#41;](use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar el formato de caracteres Unicode para importar o exportar datos &#40;SQL Server&#41;](use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
## <a name="see-also"></a>Consulte también  
 [bcp (utilidad)](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [Tipos de datos &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql)  
  
  
