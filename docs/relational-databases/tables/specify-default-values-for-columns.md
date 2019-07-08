---
title: Especificar valores predeterminados para las columnas | Microsoft Docs
ms.custom: ''
ms.date: 02/20/2019
ms.prod: sql
ms.prod_service: table-view-index, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- columns [SQL Server], defaults
- default values
ms.assetid: 64514aed-b846-407b-992e-cf813f9a1a91
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4fb94a2ae07993b1f95ab9adf97e164843aa06e7
ms.sourcegitcommit: cff8dd63959d7a45c5446cadf1f5d15ae08406d8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/05/2019
ms.locfileid: "67583003"
---
# <a name="specify-default-values-for-columns"></a>Especificar valores predeterminados para las columnas

[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

Puede usar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para especificar un valor predeterminado que se escribirá en la columna de tabla. Puede usar el Explorador de objetos de la interfaz de usuario o el control general para enviar [!INCLUDE[tsql](../../includes/tsql-md.md)].

Si no asigna un valor predeterminado a la columna y el usuario deja la columna en blanco, entonces:

- Si estableció la opción de permitir valores NULL, se insertará NULL en la columna.

- Si no se establece la opción para permitir valores NULL, la columna permanecerá en blanco, pero el usuario no podrá guardar la fila hasta que especifique un valor para la columna.

## <a name="Restrictions"></a> Limitaciones y restricciones

Antes de comenzar, tenga en cuenta las siguientes limitaciones y restricciones:

- Si la entrada del campo **Valor predeterminado** reemplaza un valor predeterminado enlazado (que se muestra sin paréntesis), se le preguntará si quiere desenlazar el valor predeterminado y sustituirlo por el nuevo.

- Para escribir una cadena de texto, incluya el valor entre comillas simples ('); no debe usar comillas dobles (") porque están reservadas para los identificadores escritos entre comillas.

- Para especificar un valor predeterminado numérico, escriba el número sin comillas.

- Para especificar un objeto o función, escriba el nombre del objeto o función sin comillas.

### <a name="Security"></a> Permisos de seguridad

Las acciones descritas en este artículo requieren el permiso ALTER en la tabla.

## <a name="SSMSProcedure"></a> Usar SSMS para especificar un valor predeterminado

Puede usar el Explorador de objetos para especificar un valor predeterminado de una columna de tabla.

### <a name="object-explorer"></a>Explorador de objetos

1. En el **Explorador de objetos**, haga clic con el botón derecho en la tabla que contenga columnas cuya escala quiera cambiar y, después, haga clic en **Diseño**.

2. Seleccione la columna para la que desea especificar un valor predeterminado.

3. En la pestaña **Propiedades de columna** , escriba el nuevo valor predeterminado en la propiedad **Valor o enlace predeterminado** .

   > [!NOTE]
   > Para especificar un valor predeterminado numérico, escriba el número. Para un objeto o función, escriba su nombre. Para un valor predeterminado alfanumérico escriba el valor entre comillas simples.

4. En el menú **Archivo** , haga clic en **Guardar**_nombre de tabla_.

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

## <a name="TsqlProcedure"></a> Usar Transact-SQL para especificar un valor predeterminado

Existen diversas formas en que puede especificar un valor predeterminado de una columna, usando SSMS para enviar T-SQL.

### <a name="alter-table-t-sql"></a>ALTER TABLE (T-SQL)

1. En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].

2. En la barra de Estándar, haga clic en **Nueva consulta**.

3. Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.

   ```sql
   CREATE TABLE dbo.doc_exz (column_a INT, column_b INT); -- Allows nulls.
   GO
   INSERT INTO dbo.doc_exz (column_a) VALUES (7);
   GO
   ALTER TABLE dbo.doc_exz
     ADD CONSTRAINT col_b_def
     DEFAULT 50 FOR column_b;
   GO
   ```

<!--
The following two T-SQL code examples were offered by 'nycdotnet' (Steve) via public PR 1660, Feb 2019.
-->

### <a name="create-table-t-sql"></a>CREATE TABLE (T-SQL)

```sql
    CREATE TABLE dbo.doc_exz (
      column_a INT,
      column_b INT DEFAULT 50);
```

### <a name="named-constraint-t-sql"></a>CONSTRAINT con nombre (T-SQL)

```sql
    CREATE TABLE dbo.doc_exz (
      column_a INT,
      column_b INT CONSTRAINT DF_doc_exz_column_b DEFAULT 50);
```

Para obtener más información, vea [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md).
