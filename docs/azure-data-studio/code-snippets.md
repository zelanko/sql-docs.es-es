---
title: Crear fragmentos de código reutilizables
titleSuffix: Azure Data Studio
description: Obtenga información sobre cómo crear y utilizar fragmentos de código SQL en Azure Data Studio
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
manager: craigg
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 2c9e4b38fceedc9a2bfe7690cab759cdc77ea8f2
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/06/2019
ms.locfileid: "65105325"
---
# <a name="create-and-use-code-snippets-to-quickly-create-transact-sql-t-sql-scripts-in-includename-sosincludesname-sos-shortmd"></a>Crear y utilizar fragmentos de código para crear rápidamente scripts de Transact-SQL (T-SQL) en [!INCLUDE[name-sos](../includes/name-sos-short.md)]

Fragmentos de código en [!INCLUDE[name-sos](../includes/name-sos-short.md)] son plantillas que facilitan la creación de bases de datos y objetos de base de datos. 

[!INCLUDE[name-sos](../includes/name-sos-short.md)] proporciona varios fragmentos de código de Transact-SQL que le ayudarán a generar rápidamente la sintaxis correcta. 

También se pueden crear fragmentos de código definido por el usuario.

## <a name="using-built-in-t-sql-code-snippets"></a>Uso de fragmentos de código integrados de T-SQL

1. Para obtener acceso a los fragmentos de código disponibles, escriba *sql* en el editor de consultas para abrir la lista:

   ![fragmentos de código](media/code-snippets/sql-snippets.png)

1. Seleccione el fragmento de código que desea usar y genera el script de T-SQL. Por ejemplo, seleccione *sqlCreateTable*:

   ![crear fragmentos de código de tabla](media/code-snippets/create-table.png)

1. Actualice los campos resaltados con sus valores específicos. Por ejemplo, reemplace *TableName* y *esquema* con los valores de la base de datos:

   ![Sustituya el campo de plantilla](media/code-snippets/table-from-snippet.png)

   Si ya no está resaltado el campo que desea cambiar (Esto ocurre cuando se mueve el cursor en el editor), haga clic en la palabra que desee cambiar y seleccione **cambie todas las apariciones**:

   ![Sustituya el campo de plantilla](media/code-snippets/change-all.png)

1. Actualizar o agregar cualquier T-SQL adicional que necesita para el fragmento de código seleccionado. Por ejemplo, actualizar *Column1*, *Column2*y agregar más columnas.


 
## <a name="creating-sql-code-snippets"></a>Crear fragmentos de código SQL 

Puede definir sus propios fragmentos de código. Para abrir el archivo de fragmento de código SQL para editarlo:

1. Abra el *paleta de comandos* (**Ctrl + Mayús + P**) y el tipo *recorte*y seleccione **preferencias: Abra los fragmentos de código de usuario**:

   ![Sustituya el campo de plantilla](media/code-snippets/user-snippets.png)

1. Seleccione **SQL**:

   > [!NOTE]
   > [!INCLUDE[name-sos](../includes/name-sos-short.md)] hereda su funcionalidad de fragmento de código de Visual Studio Code para que este artículo trata específicamente con fragmentos de código SQL. Para obtener más información, consulte [crear sus propios fragmentos](https://code.visualstudio.com/docs/editor/userdefinedsnippets) en la documentación de Visual Studio Code. 

   ![Sustituya el campo de plantilla](media/code-snippets/select-sql.png)

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
1. Abra una nueva ventana del editor de consultas haciendo **CTRL+n**.
2. Tipo **sql**, y ver los fragmentos de código de usuario de dos que acaba de agregar; *sqlCreateTable2* y *sqlSelectTop5*.

Seleccione uno de los fragmentos de código nuevo y asígnele una serie de pruebas.


## <a name="additional-resources"></a>Recursos adicionales

Para obtener información acerca del editor SQL, vea [tutorial del editor de código](tutorial-sql-editor.md).
