---
title: Usar el formato nativo para importar o exportar datos (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- native data format [SQL Server]
- data formats [SQL Server], native
ms.assetid: eb279b2f-0f1f-428f-9b8f-2a7fc495b79f
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2dee0f6a337cab7713862e662e06bb94a0b34a5d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63065761"
---
# <a name="use-native-format-to-import-or-export-data-sql-server"></a>Usar el formato nativo para importar o exportar datos (SQL Server)
  Se recomienda usar el formato nativo cuando se realice una transferencia masiva de datos entre varias instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando un archivo de datos que no contiene caracteres extendidos o de doble byte (DBCS).  
  
> [!NOTE]  
>  Para realizar una transferencia masiva de datos entre varias instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizando un archivo de datos que contenga caracteres extendidos o DBCS, debe utilizar el formato nativo Unicode. Para obtener más información, vea [Usar el formato nativo Unicode para importar o exportar datos &#40;SQL Server&#41;](use-unicode-native-format-to-import-or-export-data-sql-server.md).  
  
 El formato nativo mantiene los tipos de datos nativos de una base de datos. Está pensado para transferencias de datos de alta velocidad entre tablas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Si utiliza un archivo de formato, las tablas de origen y destino no tienen que ser idénticas. La transferencia de datos implica dos pasos:  
  
1.  Exportación masiva de datos de una tabla de origen a un archivo de datos  
  
2.  Importación masiva de datos de un archivo de datos a una tabla de destino  
  
 El uso del formato nativo entre tablas idénticas evita la conversión innecesaria de tipos de datos a y desde el formato de caracteres, lo que ahorra tiempo y espacio. No obstante, para obtener la velocidad de transferencia óptima, se realizan algunas comprobaciones relativas al formato de los datos. Para evitar problemas con los datos cargados, vea la siguiente lista de restricciones.  
  
## <a name="restrictions"></a>Restrictions  
 Para importar datos con formato nativo correctamente, asegúrese de lo siguiente:  
  
-   El archivo de datos tiene formato nativo.  
  
-   O bien la tabla de destino debe ser compatible con el archivo de datos (tiene el mismo número de columnas, el mismo tipo de datos, la misma longitud, el estado NULL, etc.) o bien debe utilizar un archivo de formato para asignar cada campo a las columnas correspondientes.  
  
    > [!NOTE]  
    >  Si importa datos de un archivo que no coincide con la tabla de destino, la operación de importación puede ser correcta pero, probablemente, los valores de los datos insertados en la tabla de destino son incorrectos. Esto se debe a que los datos del archivo se interpretan utilizando el formato de la tabla de destino. Por tanto, si hay alguna incoherencia, se insertan valores incorrectos. No obstante, en ningún caso puede tal incoherencia dar lugar a incoherencias lógicas o físicas en la base de datos.  
  
     Para obtener más información sobre cómo usar archivos de formato, vea [Archivos de formato para importar o exportar datos &#40;SQL Server&#41;](format-files-for-importing-or-exporting-data-sql-server.md).  
  
 Una importación correcta no daña la tabla de destino.  
  
## <a name="how-bcp-handles-data-in-native-format"></a>Cómo trata bcp los datos con formato nativo  
 Esta sección aborda una serie de consideraciones especiales sobre el modo en que la utilidad **bcp** exporta e importa datos con formato nativo.  
  
-   Datos que no son caracteres  
  
     La utilidad bcp utiliza el formato de datos binario interno de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para escribir datos que no son caracteres de una tabla en un archivo de datos.  
  
-   Datos `char` o `varchar`  
  
     Al principio de cada `char` o `varchar` campo, **bcp** agrega la longitud del prefijo.  
  
    > [!IMPORTANT]  
    >  Cuando se utiliza el modo nativo, de manera predeterminada, la utilidad **bcp** convierte los caracteres de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en caracteres OEM antes de copiarlos en el archivo de datos. La utilidad **bcp** convierte caracteres de un archivo de datos en caracteres ANSI antes de realizar la importación masiva de los mismos a una tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Durante estas conversiones, se pueden perder datos que tengan caracteres extendidos. Para caracteres extendidos, utilice el formato nativo Unicode o especifique una página de códigos.  
  
-   Datos `sql_variant`  
  
     Si se almacenan datos `sql_variant` como SQLVARIANT en un archivo de datos con formato nativo, los datos mantienen todas sus características. Los metadatos que registran el tipo de datos de cada valor de datos se almacenan junto con el valor de los datos. Estos metadatos se utilizan para crear de nuevo el valor de los datos con el mismo tipo de datos en una columna `sql_variant` de destino.  
  
     Si el tipo de datos de la columna de destino no es `sql_variant`, cada valor de dato se convierte al tipo de datos de la columna de destino, con las reglas normales de conversión implícita de datos. Si se produce un error durante la conversión de los datos, se revierte el lote actual. Los valores `char` y `varchar` que se transfieren entre columnas `sql_variant` pueden tener problemas de conversión de página de códigos.  
  
     Para obtener más información sobre la conversión de datos, vea [Conversiones de tipos de datos &#40;motor de base de datos&#41;](/sql/t-sql/data-types/data-type-conversion-database-engine).  
  
## <a name="command-options-for-native-format"></a>Opciones de comando para el formato nativo  
 Puede importar datos con formato nativo a una tabla usando **bcp**, BULK INSERT o INSERT... SELECT \* FROM OPENROWSET(BULK...). Para un comando **bcp** o una instrucción BULK INSERT, puede especificar el formato de datos en la línea de comandos. Para una instrucción INSERT ... SELECT * FROM OPENROWSET(BULK...), debe especificar el formato de los datos en un archivo de formato.  
  
 Las siguientes opciones de la línea de comandos admiten el formato nativo:  
  
|Comando|Opción|Descripción|  
|-------------|------------|-----------------|  
|**bcp**|**-n**|Hace que el **bcp** utilidad para usar los tipos de datos nativos de los datos.<sup> 1</sup>|  
|BULK INSERT|DATAFILETYPE **='** native **'**|Utiliza los tipos de datos nativos o nativos anchos de los datos. Tenga en cuenta que DATAFILETYPE no es necesario si el archivo de formato especifica los tipos de datos.|  
  
 <sup>1</sup> cargar nativo (**- n**) datos en un formato compatible con versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] clientes, utilice el **-V** cambie. Para obtener más información, vea [Importar datos con formato nativo y de caracteres de versiones anteriores de SQL Server](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md).  
  
 Para obtener más información, vea [bcp (utilidad)](../../tools/bcp-utility.md), [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql) u [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql).  
  
> [!NOTE]  
>  Otra posibilidad es especificar el formato por campo en un archivo de formato. Para obtener más información, vea [Archivos de formato para importar o exportar datos &#40;SQL Server&#41;](format-files-for-importing-or-exporting-data-sql-server.md).  
  
## <a name="examples"></a>Ejemplos  
 En los siguientes ejemplos se muestra el modo de exportar masivamente datos nativos con **bcp** e importar masivamente los mismos datos mediante BULK INSERT.  
  
### <a name="sample-table"></a>Tabla de ejemplo  
 Los ejemplos requieren que se cree una tabla denominada **myTestNativeData** en la base de datos de ejemplo **AdventureWorks** , bajo el esquema **dbo** . Antes de poder ejecutar los ejemplos, debe crear esta tabla. En el Editor de consultas de [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] , ejecute:  
  
```  
USE AdventureWorks;  
GO  
CREATE TABLE myTestNativeData (  
   Col1 smallint,  
   Col2 nvarchar(50),  
   Col3 nvarchar(50)  
   );   
```  
  
 Para rellenar esta tabla y ver el contenido resultante, ejecute las siguientes instrucciones:  
  
```  
INSERT INTO myTestNativeData(Col1,Col2,Col3)  
   VALUES(1,'DataField2','DataField3');  
INSERT INTO myTestNativeData(Col1,Col2,Col3)  
   VALUES(2,'DataField2','DataField3');  
GO  
SELECT Col1,Col2,Col3 FROM myTestNativeData  
  
```  
  
### <a name="using-bcp-to-bulk-export-native-data"></a>Usar bcp para exportar masivamente datos nativos  
 Para exportar datos de la tabla a un archivo de datos, use **bcp** con la opción **out** y los siguientes calificadores:  
  
|Calificadores|Descripción|  
|----------------|-----------------|  
|**-n**|Especifica tipos de datos nativos.|  
|**-T**|Especifica que la utilidad **bcp** se conecta a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con una conexión de confianza utilizando la seguridad integrada. Si no se especifica **-T**, es necesario especificar **-U** y **-P** para iniciar sesión correctamente.|  
  
 En el siguiente ejemplo se exportan masivamente datos en formato nativo desde la tabla `myTestNativeData` a un nuevo archivo de datos denominado `myTestNativeData-n.Dat`. En el símbolo del sistema de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows, especifique:  
  
```  
bcp AdventureWorks..myTestNativeData out C:\myTestNativeData-n.Dat -n -T  
  
```  
  
### <a name="using-bulk-insert-to-bulk-import-native-data"></a>Usar BULK INSERT para importar masivamente datos nativos  
 En el siguiente ejemplo se utiliza BULK INSERT para importar los datos del archivo de datos `myTestNativeData-n.Dat` en la tabla `myTestNativeData` . En el Editor de consultas de [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] , ejecute:  
  
```  
USE AdventureWorks;  
GO  
BULK INSERT myTestNativeData   
    FROM 'C:\myTestNativeData-n.Dat'   
   WITH (DATAFILETYPE='native');   
GO  
SELECT Col1,Col2,Col3 FROM myTestNativeData  
GO  
  
```  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
 **Para usar formatos de datos para la importación o exportación masivas**  
  
-   [Importar datos con formato nativo y de caracteres de versiones anteriores de SQL Server](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
-   [Usar el formato de caracteres para importar o exportar datos &#40;SQL Server&#41;](use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar el formato de caracteres Unicode para importar o exportar datos &#40;SQL Server&#41;](use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar el formato nativo Unicode para importar o exportar datos &#40;SQL Server&#41;](use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
## <a name="see-also"></a>Vea también  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [Tipos de datos &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql)   
 [sql_variant &#40;Transact-SQL&#41;](/sql/t-sql/data-types/sql-variant-transact-sql)   
 [Importar datos con formato nativo y de caracteres de versiones anteriores de SQL Server](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [Usar el formato nativo Unicode para importar o exportar datos &#40;SQL Server&#41;](use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
  
