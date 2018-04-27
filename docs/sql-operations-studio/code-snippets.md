---
title: Crear fragmentos de código en las operaciones de SQL Studio (versión preliminar) | Documentos de Microsoft
description: Obtenga información acerca de cómo crear y utilizar fragmentos de código SQL en las operaciones de SQL Studio (versión preliminar)
ms.custom: tools|sos
ms.date: 11/15/2017
ms.reviewer: alayu; erickang; sstein
ms.prod: sql
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: article
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f51c14d2c3824baa1b2730d352b94d9cfdc097bc
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="create-and-use-code-snippets-to-quickly-create-transact-sql-t-sql-scripts-in-includename-sosincludesname-sos-shortmd"></a>Crear y utilizar fragmentos de código para crear rápidamente scripts de Transact-SQL (T-SQL) en [!INCLUDE[name-sos](../includes/name-sos-short.md)]

Fragmentos de código en el código [!INCLUDE[name-sos](../includes/name-sos-short.md)] son plantillas que resulten más fácil crean bases de datos y objetos de base de datos. 

[!INCLUDE[name-sos](../includes/name-sos-short.md)] proporciona varios fragmentos de código de T-SQL que le ayudarán a generar rápidamente la sintaxis correcta. 

También se pueden crear fragmentos de código definido por el usuario.

## <a name="using-built-in-t-sql-code-snippets"></a>Usar fragmentos de código de T-SQL integrados

1. Para obtener acceso a los fragmentos de código disponibles, escriba *sql* en el editor de consultas para abrir la lista:

   ![fragmentos de código](media/code-snippets/sql-snippets.png)

1. Seleccione el fragmento de código que desea usar y genera el script de T-SQL. Por ejemplo, seleccione *sqlCreateTable*:

   ![crear fragmentos de código de tabla](media/code-snippets/create-table.png)

1. Actualizar los campos resaltados con los valores específicos. Por ejemplo, reemplace *TableName* y *esquema* con los valores de la base de datos:

   ![Reemplace el campo de plantilla](media/code-snippets/table-from-snippet.png)

   Si ya no se resalta el campo que desea cambiar (Esto ocurre cuando se mueve el cursor en el editor), haga clic en la palabra que desea cambiar y seleccione **cambie todas las apariciones**:

   ![Reemplace el campo de plantilla](media/code-snippets/change-all.png)

1. Actualizar o agregar cualquier T-SQL adicional necesario para el fragmento de código seleccionado. Por ejemplo, actualizar *Column1*, *Column2*y agregar más columnas.


 
## <a name="creating-sql-code-snippets"></a>Crear fragmentos de código SQL 

Puede definir sus propios fragmentos de código. Para abrir el archivo de fragmento de código SQL para editarlo:

1. Abra el *comando paleta* (**Mayús + Ctrl + P**) y el tipo de *recorte*y seleccione **preferencias: abra fragmentos de código de usuario**:

   ![Reemplace el campo de plantilla](media/code-snippets/user-snippets.png)

1. Seleccione **SQL**:

   > [!NOTE]
   > [!INCLUDE[name-sos](../includes/name-sos-short.md)] hereda su funcionalidad de fragmento de código de código de Visual Studio para que este artículo se describe específicamente con fragmentos de código SQL. Para obtener más información, consulte [crear sus propios fragmentos](https://code.visualstudio.com/docs/editor/userdefinedsnippets) en la documentación de Visual Studio Code. 

   ![Reemplace el campo de plantilla](media/code-snippets/select-sql.png)

1. Pegue el siguiente código en *sql.json*:

   ```sql
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
   ```

1. Guarde el archivo sql.json.
1. Abrir una nueva ventana del editor de consultas haciendo clic en **CTRL+n**.
2. Tipo de **sql**, y verá los fragmentos de código de usuario de dos que acaba de agregar; *sqlCreateTable2* y *sqlSelectTop5*.

Seleccione uno de los fragmentos de código nuevo y asígnele una serie de pruebas.


## <a name="additional-resources"></a>Recursos adicionales

Para obtener información acerca del editor SQL, vea [tutorial del editor de código](tutorial-sql-editor.md).