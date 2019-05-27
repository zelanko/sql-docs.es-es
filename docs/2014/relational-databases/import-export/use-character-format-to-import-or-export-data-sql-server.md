---
title: Usar el formato de caracteres para importar o exportar datos (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- data formats [SQL Server], character
- character formats [SQL Server]
ms.assetid: d925e66a-1a73-43cd-bc06-1cbdf8174a4d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ab658be26dc8ccbdd4e760d0b1bc835ace3b2c38
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/22/2019
ms.locfileid: "66011665"
---
# <a name="use-character-format-to-import-or-export-data-sql-server"></a>Usar el formato de caracteres para importar o exportar datos (SQL Server)
  Se recomienda utilizar el formato de caracteres al exportar datos de forma masiva a un archivo de texto que se va a utilizar en otro programa o al importar datos de forma masiva desde un archivo de texto generado por otro programa.  
  
> [!NOTE]  
>  Para transferir datos masivamente entre instancias de [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuando el archivo de datos contiene caracteres Unicode pero no contiene caracteres extendidos o DBCS, utilice el formato de caracteres Unicode. Para obtener más información, vea [Usar el formato de caracteres Unicode para importar o exportar datos &#40;SQL Server&#41;](use-unicode-character-format-to-import-or-export-data-sql-server.md).  
  
 El formato de caracteres utiliza el formato de datos de caracteres para todas las columnas. El almacenamiento de información en el formato de caracteres resulta útil si se utilizan los datos en otro programa, como hojas de cálculo, o bien cuando es necesario copiar los datos a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desde una base de datos de otro proveedor, como Oracle.  
  
## <a name="considerations-for-using-character-format"></a>Consideraciones acerca del uso del formato de caracteres  
 Al utilizar el formato de caracteres, tenga en cuenta que:  
  
-   De forma predeterminada, la utilidad **bcp** separa los campos de datos de caracteres con el carácter de tabulación y finaliza los registros con el carácter de nueva línea. Para obtener más información sobre cómo especificar otros terminadores, vea [Especificar terminadores de campo y de fila &#40;SQL Server&#41;](specify-field-and-row-terminators-sql-server.md).  
  
-   De forma predeterminada, antes de la exportación o importación masiva de los datos en modo de caracteres, se realizan las conversiones siguientes:  
  
    |Dirección de la operación masiva|Conversión|  
    |---------------------------------|----------------|  
    |Exportar|Convierte los datos en representaciones de caracteres. Si se solicita de forma explícita, los datos se convierten a la página de códigos solicitada para las columnas de caracteres. Si no se especifica ninguna página de códigos, los datos de caracteres se convierten mediante la página de códigos OEM del equipo cliente.|  
    |Importar|Convierte los datos de caracteres en representaciones nativas, cuando es necesario, y traduce los datos de caracteres de la página de códigos del cliente a la página de códigos de las columnas de destino.|  
  
-   Para evitar la pérdida de caracteres extendidos durante la conversión, utilice el formato de caracteres Unicode o especifique una página de códigos.  
  
-   Cualquier dato `sql_variant` almacenado en un archivo de formato de caracteres se almacena sin metadatos. Cada valor de dato se convierte al formato `char` según las reglas de conversión implícita de datos. Cuando los datos se importan en la columna `sql_variant`, se importan como `char`. Cuando los datos se importan en una columna con un tipo de datos diferente de `sql_variant`, se convierten desde `char` mediante una conversión implícita. Para obtener más información sobre la conversión de datos, vea [Conversiones de tipos de datos &#40;motor de base de datos&#41;](/sql/t-sql/data-types/data-type-conversion-database-engine).  
  
-   El **bcp** utilidad exportaciones `money` valores como archivos de datos de formato de caracteres con cuatro dígitos después del separador decimal y sin símbolos de agrupación de dígitos como separadores de coma. Por ejemplo, una columna `money` que contenga el valor 1.234.567,123456 se copiará de forma masiva en un archivo de datos como la cadena de caracteres 1234567,1235.  
  
## <a name="command-options-for-character-format"></a>Opciones de comando para el formato de caracteres  
 Puede importar datos en formato de caracteres en una tabla usando **bcp**, BULK INSERT o INSERT ... SELECT \* FROM OPENROWSET(BULK...). Para un comando **bcp** o una instrucción BULK INSERT, puede especificar el formato de datos en la línea de comandos. Para una instrucción INSERT ... SELECT * FROM OPENROWSET(BULK...), debe especificar el formato de los datos en un archivo de formato.  
  
 El formato de caracteres puede usarse con las siguientes opciones de la línea de comandos:  
  
|Comando|Opción|Descripción|  
|-------------|------------|-----------------|  
|**bcp**|**-c**|Hace que el **bcp** utilidad use datos de caracteres.<sup> 1</sup>|  
|BULK INSERT|DATAFILETYPE **='char'**|Utiliza el formato de caracteres al importar datos masivamente.|  
  
 <sup>1</sup> para cargar el carácter (**- c**) datos en un formato compatible con versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] clientes, utilice el **-V** cambie. Para obtener más información, vea [Importar datos con formato nativo y de caracteres de versiones anteriores de SQL Server](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md).  
  
 Para obtener más información, vea [bcp (utilidad)](../../tools/bcp-utility.md), [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql) u [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql).  
  
> [!NOTE]  
>  Otra posibilidad es especificar el formato por campo en un archivo de formato. Para obtener más información, vea [Archivos de formato para importar o exportar datos &#40;SQL Server&#41;](format-files-for-importing-or-exporting-data-sql-server.md).  
  
## <a name="examples"></a>Ejemplos  
 En los siguientes ejemplos se muestra el modo de exportar masivamente datos de caracteres con **bcp** e importar masivamente los mismos datos mediante BULK INSERT.  
  
### <a name="sample-table"></a>Tabla de ejemplo  
 Los ejemplos requieren que se cree una tabla denominada **myTestCharData** en la base de datos de ejemplo **AdventureWorks** , bajo el esquema **dbo** . Antes de poder ejecutar los ejemplos, debe crear esta tabla. Para ello, en el Editor de consultas de [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] , ejecute:  
  
```  
USE AdventureWorks;  
GO  
CREATE TABLE myTestCharData (  
   Col1 smallint,  
   Col2 nvarchar(50),  
   Col3 nvarchar(50)  
   );   
```  
  
 Para rellenar esta tabla y ver el contenido resultante, ejecute las siguientes instrucciones:  
  
```  
INSERT INTO myTestCharData(Col1,Col2,Col3)  
   VALUES(1,'DataField2','DataField3');  
INSERT INTO myTestCharData(Col1,Col2,Col3)  
   VALUES(2,'DataField2','DataField3');  
GO  
SELECT Col1,Col2,Col3 FROM myTestCharData  
  
```  
  
### <a name="using-bcp-to-bulk-export-character-data"></a>Usar bcp para exportar de forma masiva datos de caracteres  
 Para exportar datos de la tabla a un archivo de datos, use **bcp** con la opción **out** y los siguientes calificadores:  
  
|Calificadores|Descripción|  
|----------------|-----------------|  
|**-c**|Especifica el formato de caracteres.|  
|**-t** `,`|Especifica una coma (`,`) como terminador de campo.<br /><br /> Nota: El terminador de campo predeterminado es el carácter de tabulación (\t). Para obtener más información, vea [Especificar terminadores de campo y de fila &#40;SQL Server&#41;](specify-field-and-row-terminators-sql-server.md).|  
|**-T**|Especifica que la utilidad **bcp** se conecta a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con una conexión de confianza utilizando la seguridad integrada. Si no se especifica **-T**, es necesario especificar **-U** y **-P** para iniciar sesión correctamente.|  
  
 En el siguiente ejemplo se exportan masivamente datos en formato de caracteres desde la tabla `myTestCharData` en un nuevo archivo de datos denominado `myTestCharData-c.Dat` que utiliza la coma (,) como terminador de campo. En el símbolo del sistema de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows, especifique:  
  
```  
bcp AdventureWorks..myTestCharData out C:\myTestCharData-c.Dat -c -t, -T  
  
```  
  
### <a name="using-bulk-insert-to-bulk-import-character-data"></a>Usar BULK INSERT para importar de forma masiva datos de caracteres  
 En el siguiente ejemplo se utiliza BULK INSERT para importar los datos del archivo de datos `myTestCharData-c.Dat` en la tabla `myTestCharData` . En el Editor de consultas de [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] , ejecute:  
  
```  
USE AdventureWorks;  
GO  
BULK INSERT myTestCharData   
   FROM 'C:\myTestCharData-c.Dat'   
   WITH (  
      DATAFILETYPE='char',  
      FIELDTERMINATOR=','  
   );   
GO  
SELECT Col1,Col2,Col3 FROM myTestCharData;  
GO  
  
```  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
 **Para usar formatos de datos para la importación o exportación masivas**  
  
-   [Importar datos con formato nativo y de caracteres de versiones anteriores de SQL Server](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
-   [Usar el formato nativo para importar o exportar datos &#40;SQL Server&#41;](use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar el formato de caracteres Unicode para importar o exportar datos &#40;SQL Server&#41;](use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar el formato nativo Unicode para importar o exportar datos &#40;SQL Server&#41;](use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
## <a name="see-also"></a>Vea también  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [Tipos de datos &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql)   
 [Importar datos con formato nativo y de caracteres de versiones anteriores de SQL Server](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
  
