---
title: Especificar formatos de datos por razones de compatibilidad mediante bcp (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: data-movement
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- bulk exporting [SQL Server], compatibility
- bulk importing [SQL Server], compatibility
- compatibility [SQL Server], data formats
- data formats [SQL Server], compatibility
- bcp utility [SQL Server], compatibility
ms.assetid: cd5fc8c8-eab1-4165-9468-384f31e53f0a
caps.latest.revision: 36
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 42266e1f4ab136045c16d1e0f41d6ae802c3f1c7
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37154546"
---
# <a name="specify-data-formats-for-compatibility-when-using-bcp-sql-server"></a>Especificar formatos de datos por razones de compatibilidad mediante bcp (SQL Server)
  En este tema se describe los atributos de formato de datos, mensajes específicos de los campos y almacenamiento de datos de campo por campo en un archivo de formato no xml de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `bcp` comando. Comprenderlo puede ser útil cuando se realiza una exportación masiva datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para importarlos masivamente en otro programas, como por ejemplo otro programa de base de datos. Los formatos de datos predeterminados (nativo, carácter o Unicode) de la tabla de origen podrían ser incompatibles con la disposición de los datos esperada por el otro programa. Si existe una incompatibilidad, al exportar los datos, debe describirse su disposición.  
  
> [!NOTE]  
>  Si no está familiarizado con los formatos de datos para importarlos o exportarlos, vea [Formatos de datos para importación en bloque o exportación masiva &#40;SQL Server&#41;](data-formats-for-bulk-import-or-bulk-export-sql-server.md).  
  
 **En este tema:**  
  
-   [Atributo de formato de datos bcp](#bcpDataFormatAttr)  
  
-   [Información general sobre los mensajes específicos de los campos](#FieldSpecificPrompts)  
  
-   [Almacenar datos campo por campo en un archivo de formato no XML](#FieldByFieldNonXmlFF)  
  
-   [Tareas relacionadas](#RelatedTasks)  
  
##  <a name="bcpDataFormatAttr"></a> Atributo de formato de datos bcp  
 El comando `bcp` permite especificar la estructura de cada campo en función de los siguientes atributos de formato de datos:  
  
-   tipo de almacenamiento en archivo  
  
     El *tipo de almacenamiento en archivo* describe cómo se almacenan los datos en el archivo de datos. Datos se pueden exportar a un archivo de datos como el tipo de tabla de base de datos (formato nativo), como su representación en caracteres (formato de caracteres) o como cualquier tipo de datos donde se admite la conversión implícita; Por ejemplo, si copia una `smallint` como un `int`. Los tipos de datos definidos por el usuario se exportan como sus tipos base correspondientes. Para obtener más información, vea [Especificar el tipo de almacenamiento en archivo mediante bcp &#40;SQL Server&#41;](specify-file-storage-type-by-using-bcp-sql-server.md).  
  
-   Longitud del prefijo  
  
     Para proporcionar el almacenamiento en archivo más compacto para exportar de forma masiva datos en formato nativo a un archivo de datos, el comando `bcp` precede cada campo con uno o varios caracteres que indican la longitud del campo. Estos caracteres se denominan *caracteres de prefijo de longitud*. Para obtener más información, vea [Especificar la longitud de prefijo en los archivos de datos mediante bcp &#40;SQL Server&#41;](specify-prefix-length-in-data-files-by-using-bcp-sql-server.md).  
  
-   Longitud de campo  
  
     La longitud de campo indica el número máximo de caracteres necesarios para representar los datos en formato de carácter. La longitud de campo ya se conoce si los datos se almacenan en el formato nativo. Para obtener más información, vea [Especificar la longitud de campo mediante bcp &#40;SQL Server&#41;](specify-field-length-by-using-bcp-sql-server.md).  
  
-   Terminador de campo  
  
     En el caso de campos de datos de caracteres, los caracteres de terminación le permiten marcar el final de cada campo en un archivo de datos (usando un *terminador de campo*) y el final de cada fila (usando un *terminador de fila*). Los caracteres de terminación son un modo de indicar a los programas que leen el archivo de datos dónde termina un campo o una fila y dónde comienza otro. Para obtener más información, vea [Specify Field and Row Terminators &#40;SQL Server&#41;](specify-field-and-row-terminators-sql-server.md).  
  
##  <a name="FieldSpecificPrompts"></a> Información general acerca de peticiones específicas de campos  
 Si un interactivo `bcp` comando contiene el **en** o **out** opción pero no contiene el modificador de archivo de formato (**-f**) o cambiar de un formato de datos () **- n**, **- c**, **-w**, o **-N**), cada columna de la tabla de origen o destino, el comando solicita para cada uno de los anteriores atributos, a su vez. En cada mensaje, el `bcp` comando proporciona un valor predeterminado basado en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de datos de la columna de tabla. Si acepta el valor predeterminado de todos los mensajes, se obtiene el mismo resultado que si especifica un formato nativo (**-n**) en la línea de comandos. Cada mensaje muestra un valor predeterminado entre corchetes: [*default*]. Para aceptar el valor predeterminado que se muestra, presione la tecla ENTRAR. Para especificar un valor distinto del predeterminado, escriba el nuevo valor cuando en el mensaje.  
  
### <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se usa el `bcp` comando para la masiva exportar los datos de la `HumanResources.myTeam` tabla interactivamente al `myTeam.txt` archivo. Antes de que pueda ejecutar el ejemplo, debe crear esta tabla. Para obtener más información sobre la tabla y cómo crearla, vea [Tabla de ejemplo HumanResources.myTeam &#40;SQL Server&#41;](humanresources-myteam-sample-table-sql-server.md).  
  
 El comando especifica un archivo de formato ni un tipo de datos, provocando `bcp` para solicitar información de formato de datos. En el símbolo del sistema de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows, especifique:  
  
```  
bcp AdventureWorks.HumanResources.myTeam out myTeam.txt -T  
```  
  
 Para cada columna, bcp solicita los valores específicos de los campos. El siguiente ejemplo muestra las peticiones específicas de los campos de las columnas `EmployeeID` y `Name` de la tabla y sugiere el tipo de almacenamiento de archivo predeterminado (el formato nativo) para cada columna. Las longitudes de prefijo de la columna `EmployeeID` y `Name` son 0 y 2, respectivamente. El usuario especifica una coma (`,`) como terminador de cada campo.  
  
 `Enter the file storage type of field EmployeeID [smallint]:`  
  
 `Enter prefix-length of field EmployeeID [0]:`  
  
 `Enter field terminator [none]:,`  
  
 `Enter the file storage type of field Name [nvarchar]:`  
  
 `Enter prefix length of field Name [2]:`  
  
 `Enter field terminator [none]:,`  
  
 `.`  
  
 `.`  
  
 `.`  
  
 Se muestran en orden peticiones equivalentes (cuando se necesitan) para cada una de las columnas de la tabla.  
  
##  <a name="FieldByFieldNonXmlFF"></a> Almacenar datos campo a campo en un formato de archivo no XML  
 Después de todo se especifican las columnas de la tabla, el `bcp` comando le pide que, opcionalmente, generar un archivo de formato no XML que almacena la información campo a campo recientemente suministrada (vea el ejemplo anterior). Si elige generar un archivo de formato, puede hacerlo siempre que exporte datos fuera de esa tabla o importe datos estructurados de manera similar en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Puede utilizar el archivo de formato para importar datos de manera masiva desde el archivo de datos en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o para exportar datos de manera masiva desde la tabla sin la necesidad de volver a especificar el formato. Para obtener más información, vea [Archivos de formato para importar o exportar datos &#40;SQL Server&#41;](format-files-for-importing-or-exporting-data-sql-server.md).  
  
 En el siguiente ejemplo se crea un archivo de formato no XML llamado `myFormatFile.fmt`:  
  
 `Do you want to save this format information in a file? [Y/n] y`  
  
 `Host filename: [bcp.fmt]myFormatFile.fmt`  
  
 El nombre predeterminado del archivo de formato es bcp.fmt, pero puede especificar un nombre de archivo diferente si así lo decide.  
  
> [!NOTE]  
>  En el caso de un archivo de datos que use un solo formato de datos para su tipo de almacenamiento de archivo, por ejemplo, un formato de caracteres o un formato nativo, puede crear rápidamente un archivo de formato sin exportar o importar datos usando la opción **format** . Este enfoque tiene las ventajas de resultar sencillo y permitirle crear un archivo de formato XML o no XML. Para obtener más información, vea [Crear un archivo de formato &#40;SQL Server&#41;](create-a-format-file-sql-server.md).  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
  
-   [Especificar el tipo de almacenamiento en archivo mediante bcp &#40;SQL Server&#41;](specify-file-storage-type-by-using-bcp-sql-server.md)  
  
-   [Especificar la longitud de prefijo en los archivos de datos mediante bcp &#40;SQL Server&#41;](specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)  
  
-   [Especificar la longitud de campo mediante bcp &#40;SQL Server&#41;](specify-field-length-by-using-bcp-sql-server.md)  
  
-   [Especificar terminadores de campo y de fila &#40;SQL Server&#41;](specify-field-and-row-terminators-sql-server.md)  
  
## <a name="related-content"></a>Contenido relacionado  
 Ninguno.  
  
## <a name="see-also"></a>Vea también  
 [Importar y exportar datos en bloque &#40;SQL Server&#41;](bulk-import-and-export-of-data-sql-server.md)   
 [Formatos de datos para importación en bloque o exportación masiva &#40;SQL Server&#41;](data-formats-for-bulk-import-or-bulk-export-sql-server.md)   
 [bcp (utilidad)](../../tools/bcp-utility.md)   
 [Tipos de datos &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql)  
  
  
