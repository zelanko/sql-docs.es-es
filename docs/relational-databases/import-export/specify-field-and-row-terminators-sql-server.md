---
title: Especificar terminadores de campo y de fila (SQL Server) | Microsoft Docs
ms.custom: 
ms.date: 08/10/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-bulk-import-export
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- bcp utility [SQL Server], terminators
- field terminators [SQL Server]
- data formats [SQL Server], terminators
- row terminators [SQL Server]
- terminators [SQL Server]
ms.assetid: f68b6782-f386-4947-93c4-e89110800704
caps.latest.revision: 39
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Active
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 42c2ee3fe98d6c6fc35d2417469bc3eec9fddd8c
ms.contentlocale: es-es
ms.lasthandoff: 07/31/2017

---
# <a name="specify-field-and-row-terminators-sql-server"></a>Especificar terminadores de campo y de fila (SQL Server)
  En los campos de datos de caracteres, los caracteres de terminación opcionales permiten marcar el final de cada campo de un archivo de datos con un *terminador de campo* y el final de cada fila con un *terminador de fila*. Los caracteres de terminación son una forma de indicar a los programas que leen el archivo de datos dónde termina un campo o una fila y dónde comienza otro.  
  
> [!IMPORTANT]  
>  Cuando utilice el formato nativo o nativo Unicode, use prefijos de longitud en lugar de terminadores de campo. Los datos de formato nativo pueden entrar en conflicto con los terminadores, ya que un archivo de datos de formato nativo se almacena en el formato de datos binario interno de [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="characters-supported-as-terminators"></a>Caracteres admitidos como terminadores  
 El comando **bcp** , la instrucción BULK INSERT y el proveedor de conjuntos de filas BULK OPENROWSET admiten una serie de caracteres como terminadores de campo o de fila y siempre buscan la primera instancia de cada terminador. La siguiente tabla enumera los caracteres admitidos como terminadores.  
  
|Carácter de terminación|Indicado por|  
|---------------------------|------------------|  
|Pestaña|\t<br /><br /> Terminador de campo predeterminado.|  
|Carácter de nueva línea|\n<br /><br /> Terminador de fila predeterminado.|  
|Retorno de carro/avance de línea|\r|  
|Barra diagonal inversa*|\\\|  
|Terminador NULL (terminador invisible)**|\0|  
|Cualquier carácter imprimible (los caracteres de control no se pueden imprimir, excepto los valores NULL, tabulaciones, caracteres de nueva línea y retornos de carro)|(*, A, t, l, etc.)|  
|Una cadena de hasta 10 caracteres imprimibles, incluidos algunos o todos los terminadores enumerados anteriormente|(**\t\*\*, end, !!!!!!!!!!, \t—\n, etc.)|  
  
 *Solo pueden usarse los caracteres t, n, r, 0 y '\0' con el carácter de escape de barra diagonal inversa para crear un carácter de control.  
  
 **Aunque el carácter de control NULL (\0) no sea visible al imprimir, es un carácter distintivo en el archivo de datos. Esto significa que el uso del carácter de control NULL como terminador de campo o de fila es diferente a no tener ningún terminador de campo o de fila.  
  
> [!IMPORTANT]  
>  Si en los datos hay un carácter terminador, se interpreta como un terminador, no como datos, y se interpreta que los datos posteriores a ese carácter pertenecen al campo o registro siguiente. Por lo tanto, elija los terminadores con atención para asegurarse de que nunca aparezcan en los datos. Por ejemplo, un terminador de campo que funcione como suplente inferior no resultaría una buena opción para un terminador de campo si los datos contienen dicho suplente inferior.  
  
## <a name="using-row-terminators"></a>Usar terminadores de fila  
 El terminador de fila puede ser el mismo carácter que el terminador del último campo. Sin embargo, normalmente resulta útil un terminador de fila distinto. Por ejemplo, para generar un resultado en formato tabular, termine el último campo de cada fila con el carácter de nueva línea (\n) y todos los demás campos con el carácter de tabulación (\t). Para colocar cada registro de datos en su propia línea en el archivos de datos, especifique la combinación \r\n como terminador de fila.  
  
> [!NOTE]  
>  Cuando usa **bcp** en modo interactivo y especifica \n (nueva línea) como terminador de fila, **bcp** antepondrá automáticamente el carácter \r (retorno de carro) como prefijo, lo que genera un terminador de fila \r\n.  
  
## <a name="specifying-terminators-for-bulk-export"></a>Especificar terminadores para la exportación masiva  
 Cuando realiza una exportación masiva de datos **char** o **nchar** y quiere usar un terminador no predeterminado, deberá especificar el terminador en el comando **bcp** . Los terminadores se pueden especificar de cualquiera de las siguientes maneras:  
  
-   Con un archivo de formato que especifica el terminador campo a campo.  
  
    > [!NOTE]  
    >  Para obtener más información sobre cómo usar archivos de formato, vea [Archivos de formato para importar o exportar datos &#40;SQL Server&#41;](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md).  
  
-   Sin un archivo de formato, existen las alternativas siguientes:  
  
    -   Usar el modificador **-t** para especificar el terminador de campo en todos los campos, excepto el último campo de la fila, y usar el modificador **-r** para especificar un terminador de fila.  
  
    -   Usar un modificador de formato de caracteres (**-c** o **-w**) sin el modificador **-t** , lo que establece el carácter de tabulación, \t, como terminador de campo. Esto equivale a especificar **-t**\t.  
  
        > [!NOTE]  
        >  Si se especifica el modificador **-n** (datos nativos) o **-N** (nativos Unicode), no se insertan los terminadores.  
  
    -   Si un comando **bcp** interactivo contiene la opción **in** o **out** sin el modificador de archivo de formato (**-f**) ni un modificador de formato de datos (**-n**, **-c**, **-w**o **-N**), y ha decidido no especificar la longitud de prefijo ni la longitud de campo, el comando solicita el terminador de cada campo, con el valor predeterminado "none":  
  
         `Enter field terminator [none]:`  
  
         Generalmente, el valor predeterminado es una opción apropiada. Sin embargo, para los campos de datos **char** o **nchar** , vea la siguiente subsección, "Directrices para utilizar terminadores". Para obtener un ejemplo que muestra esta solicitud en contexto, vea [Especificar formatos de datos por razones de compatibilidad mediante bcp &#40;SQL Server&#41;](../../relational-databases/import-export/specify-data-formats-for-compatibility-when-using-bcp-sql-server.md).  
  
        > [!NOTE]  
        >  Después de que se especifiquen de forma interactiva todos los campos de un comando **bcp**, el comando solicita que guarde sus respuestas para cada campo en un archivo que no tenga el formato XML. Para obtener más información sobre los archivos de formato no XML, vea [Archivos de formato no XML &#40;SQL Server&#41;](../../relational-databases/import-export/non-xml-format-files-sql-server.md).  
  
### <a name="guidelines-for-using-terminators"></a>Directrices para utilizar terminadores  
 En algunas situaciones, un terminador resulta útil para un campo de datos **char** o **nchar** . Por ejemplo:  
  
-   En el caso de una columna de datos que contiene un valor NULL de un archivo de datos que se va a importar a un programa que no entiende la información sobre la longitud de prefijo.  
  
     Cualquier columna de datos que contenga un valor NULL se considera de longitud variable. En ausencia de longitudes de prefijo, se necesita un terminador para identificar el final de un campo NULL, lo que garantiza la correcta interpretación de los datos.  
  
-   En el caso de una columna de longitud fija larga cuyo espacio solo se utiliza parcialmente en numerosas filas.  
  
     En este caso, si se especifica un terminador, se puede minimizar el espacio de almacenamiento, lo que permitiría que el campo fuera tratado como un campo de longitud variable.  
  
### <a name="examples"></a>Ejemplos  
 En este ejemplo se exportan de forma masiva los datos de la tabla `AdventureWorks.HumanResources.Department` al archivo de datos `Department-c-t.txt` usando el formato de caracteres, con una coma como terminador de campo y el carácter de nueva línea (\n) como terminador de fila.  
  
 El comando **bcp** contiene los siguientes modificadores.  
  
|Switch|Descripción|  
|------------|-----------------|  
|**-c**|Especifica que los campos de datos se cargarán como datos de caracteres.|  
|**-t** `,`|Especifica una coma (,) como terminador de campo.|  
|**-r** \n|Especifica el terminador de fila como un carácter de nueva línea. Terminador de fila predeterminado, por lo que especificarlo es opcional.|  
|**-T**|Especifica que la utilidad **bcp** se conecta a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con una conexión de confianza utilizando la seguridad integrada. Si no se especifica **-T** , es necesario especificar **-U** y **-P** para iniciar sesión correctamente.|  
  
 Para obtener más información, consulte [bcp Utility](../../tools/bcp-utility.md).  
  
 En el símbolo del sistema de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows, especifique:  
  
```cmd
bcp AdventureWorks.HumanResources.Department out C:\myDepartment-c-t.txt -c -t, -r \n -T  
```  
  
 Esto crea `Department-c-t.txt`, que contiene 16 registros con cuatro campos cada uno. Los campos se separan mediante una coma.  
  
## <a name="specifying-terminators-for-bulk-import"></a>Especificar terminadores para la importación masiva  
 Cuando realice una importación de datos en bloque **char** o **nchar** , el comando de importación en bloque debe reconocer los terminadores que se usan en el archivo de datos. La forma de especificar los terminadores depende del comando de importación masiva, tal como se indica a continuación:  
  
-   **bcp**  
  
     La especificación de terminadores para una operación de importación utiliza la misma sintaxis que para una operación de exportación. Para obtener más información, vea "Especificar terminadores para la exportación masiva" anteriormente en este tema.  
  
-   BULK INSERT  
  
     Los terminadores se pueden especificar para campos individuales en un archivo de formato o para todo el archivo de datos mediante los calificadores que figuran en la siguiente tabla:  
  
    |Qualifier|Descripción|  
    |---------------|-----------------|  
    |FIELDTERMINATOR **='***field_terminator***'**|Especifica el terminador de campo que se utilizará para los archivos de caracteres y de caracteres Unicode.<br /><br /> El valor predeterminado es \t (carácter de tabulación).|  
    |ROWTERMINATOR **='***row_terminator***'**|Especifica el terminador de fila que se utilizará para los archivos de caracteres y de caracteres Unicode.<br /><br /> El valor predeterminado es \n (carácter de nueva línea).|  
  
     Para obtener más información, vea [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md).  
  
-   INSERT ... SELECT * FROM OPENROWSET(BULK...)  
  
     Para el proveedor de conjuntos de filas BULK OPENROWSET, los terminadores solo se pueden especificar en el archivo de formato (necesario excepto para tipos de datos de objetos grandes). Si un archivo de caracteres utiliza un terminador no predeterminado, debe definirse en el archivo de formato. Para obtener más información, vea [Crear un archivo de formato &#40;SQL Server&#41;](../../relational-databases/import-export/create-a-format-file-sql-server.md) y [Usar un archivo de formato para importar datos en bloque &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md).  
  
     Para obtener más información sobre la cláusula OPENROWSET BULK, vea [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md).  
  
### <a name="examples"></a>Ejemplos  
 En los ejemplos de esta sección se importan de forma masiva caracteres del archivo de datos `Department-c-t.txt` creado en el ejemplo anterior en la tabla `myDepartment` de la base de datos de ejemplo [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] . Antes de poder ejecutar los ejemplos, debe crear esta tabla. Para crear esta tabla en el esquema **dbo** , en el Editor de consultas de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , ejecute el siguiente código:  
  
```sql  
USE AdventureWorks;  
GO  
DROP TABLE myDepartment;  
CREATE TABLE myDepartment   
(DepartmentID smallint,  
Name nvarchar(50),  
GroupName nvarchar(50) NULL,  
ModifiedDate datetime not NULL CONSTRAINT DF_AddressType_ModifiedDate DEFAULT (GETDATE())  
);  
GO 
```  
  
#### <a name="a-using-bcp-to-interactively-specify-terminators"></a>A. Usar bcp para especificar terminadores interactivamente  
 En el ejemplo siguiente se importa de forma masiva el archivo de datos `Department-c-t.txt` mediante un comando `bcp` . Este comando utiliza los mismos modificadores de comando que el comando de exportación masiva. Para obtener más información, vea "Especificar terminadores para la exportación masiva" anteriormente en este tema.  
  
 En el símbolo del sistema de Windows, especifique:  
  
```cmd
bcp AdventureWorks..myDepartment in C:\myDepartment-c-t.txt -c -t , -r \n -T  
```  
  
#### <a name="b-using-bulk-insert-to-interactively-specify-terminators"></a>B. Usar BULK INSERT para especificar terminadores interactivamente  
 En el ejemplo siguiente se importa de forma masiva el archivo de datos `Department-c-t.txt` mediante una instrucción `BULK INSERT` que utiliza los calificadores que figuran en la siguiente tabla:  
  
|Opción|Attribute|  
|------------|---------------|  
|DATAFILETYPE **='**char**'**|Especifica que los campos de datos se cargarán como datos de caracteres.|  
|FIELDTERMINATOR **='**`,`**'**|Especifica una coma (`,`) como terminador de campo.|  
|ROWTERMINATOR **='**`\n`**'**|Especifica el terminador de fila como un carácter de nueva línea.|  
  
 En el Editor de consultas de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , ejecute el siguiente código:  
  
```sql  
USE AdventureWorks;  
GO  
BULK INSERT myDepartment FROM 'C:\myDepartment-c-t.txt'  
   WITH (  
      DATAFILETYPE = 'char',  
      FIELDTERMINATOR = ',',  
      ROWTERMINATOR = '\n'  
);  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [Especificar la longitud de campo mediante bcp &#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-length-by-using-bcp-sql-server.md)   
 [Especificar la longitud de prefijo en los archivos de datos mediante bcp &#40;SQL Server&#41;](../../relational-databases/import-export/specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)   
 [Especificar el tipo de almacenamiento en archivo mediante bcp &#40;SQL Server&#41;](../../relational-databases/import-export/specify-file-storage-type-by-using-bcp-sql-server.md)  
  
  

