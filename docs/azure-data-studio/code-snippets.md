---
title: Creación de fragmentos de código reutilizables
description: Obtenga información sobre cómo crear y usar fragmentos de código de SQL en Azure Data Studio
ms.prod: azure-data-studio
ms.technology: ''
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu, sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 8e2c6883840513fb9f09f8dc58080d36402bdf9f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85774697"
---
# <a name="create-and-use-code-snippets-to-quickly-create-transact-sql-t-sql-scripts-in-azure-data-studio"></a>Creación y uso de fragmentos de código para crear rápidamente scripts de Transact-SQL (T-SQL) en Azure Data Studio

Los fragmentos de código en Azure Data Studio son plantillas que permiten crear fácilmente bases de datos y objetos de bases de datos. 

Azure Data Studio proporciona varios fragmentos de código de T-SQL para ayudarle a generar rápidamente la sintaxis correcta. 

También se pueden crear fragmentos de código definidos por el usuario.

## <a name="using-built-in-t-sql-code-snippets"></a>Usar fragmentos de código de T-SQL integrados

1. Para acceder a los fragmentos de código disponibles, escriba *sql* en el editor de consultas para abrir la lista:

   ![fragmentos de código](media/code-snippets/sql-snippets.png)

1. Seleccione el fragmento de código que quiera usar y se generará el script de T-SQL. Por ejemplo, seleccione *sqlCreateTable*:

   ![crear fragmentos de código de tabla](media/code-snippets/create-table.png)

1. Actualice los campos resaltados con los valores específicos. Por ejemplo, reemplace *TableName* y *Schema* por los valores de su base de datos:

   ![reemplazar campo de plantilla](media/code-snippets/table-from-snippet.png)

   Si el campo que quiere cambiar ya no está resaltado (esto puede ocurrir si desplaza el cursor por el editor), haga clic con el botón derecho en la palabra que quiera cambiar y seleccione **Cambiar todas las repeticiones**:

   ![reemplazar campo de plantilla](media/code-snippets/change-all.png)

1. Actualice o agregue las instrucciones T-SQL que necesite para el fragmento de código seleccionado. Por ejemplo, actualice *Column1* y *Column2*, y agregue más columnas.


 
## <a name="creating-sql-code-snippets"></a>Crear fragmentos de código de SQL 

Puede definir sus propios fragmentos de código. Para abrir el archivo de fragmento de código de SQL y editarlo:

1. Abra la *Paleta de comandos* (**Mayús+Ctrl+P**), escriba *snip* y seleccione **Preferencias: abrir fragmentos de código del usuario**:

   ![reemplazar campo de plantilla](media/code-snippets/user-snippets.png)

1. Seleccione **SQL**:

   > [!NOTE]
   > Azure Data Studio hereda la función de fragmentos de código de Visual Studio Code, ya que en este artículo se explica específicamente el uso de fragmentos de código de SQL. Para obtener más información, vea [Creación de sus propios fragmento de código](https://code.visualstudio.com/docs/editor/userdefinedsnippets) en la documentación de Visual Studio Code. 

   ![reemplazar campo de plantilla](media/code-snippets/select-sql.png)

1. Pegue el código siguiente en *sql.json*:

   ```sql
   {
   "Select top 5": {
    "prefix": "sqlSelectTop5",
    "body": "SELECT TOP 5 * FROM ${1:TableName}",
    "description": "User-defined snippet example 1"
    },
    "Create Table snippet":{
    "prefix": "sqlCreateTable2",
    "body": [
    "-- Create a new table called '${1:TableName}' in schema '${2:SchemaName}'",
    "-- Drop the table if it already exists",
    "IF OBJECT_ID('$2.$1', 'U') IS NOT NULL",
    "DROP TABLE $2.$1",
    "GO",
    "-- Create the table in the specified schema",
    "CREATE TABLE $2.$1",
    "(",
    "   $1Id INT NOT NULL PRIMARY KEY, -- primary key column",
    "   Column1 [NVARCHAR](50) NOT NULL,",
    "   Column2 [NVARCHAR](50) NOT NULL",
    "   -- specify more columns here",
    ");",
    "GO"
    ],
   "description": "User-defined snippet example 2"
   }
   }
   ```

1. Guarde el archivo sql.json.
1. Presione **Ctrl+N** para abrir una nueva ventana del editor de consultas.
2. Escriba **sql**; verá los dos fragmentos de código del usuario que acaba de agregar: *sqlCreateTable2* y *sqlSelectTop5*.

Seleccione uno de los nuevos fragmentos de código y ejecútelo a modo de prueba.


## <a name="additional-resources"></a>Recursos adicionales

Para obtener información sobre el editor de SQL, vea [Tutorial del editor de código](tutorial-sql-editor.md).
