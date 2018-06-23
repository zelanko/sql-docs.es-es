---
title: Establecer o cambiar la intercalación de columnas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- tempdb database [SQL Server], collations
- collations [SQL Server], column
ms.assetid: d7a9638b-717c-4680-9b98-8849081e08be
caps.latest.revision: 29
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 3de84f26e894f00760a45d5e65769c0db8d4b009
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36103805"
---
# <a name="set-or-change-the-column-collation"></a>Establecer o cambiar la intercalación de columnas
  Puede invalidar la intercalación de base de datos para `char`, `varchar`, `text`, `nchar`, `nvarchar`, y `ntext` datos especificando una intercalación diferente para una columna concreta de una tabla y utilizando uno de los siguientes:  
  
-   La cláusula COLLATE de [CREATE TABLE](/sql/t-sql/statements/create-table-transact-sql) y [ALTER TABLE](/sql/t-sql/statements/alter-table-transact-sql). Por ejemplo:  
  
    ```  
    CREATE TABLE dbo.MyTable  
      (PrimaryKey   int PRIMARY KEY,  
       CharCol      varchar(10) COLLATE French_CI_AS NOT NULL  
      );  
    GO  
    ALTER TABLE dbo.MyTable ALTER COLUMN CharCol  
                varchar(10)COLLATE Latin1_General_CI_AS NOT NULL;  
    GO  
    ```  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para obtener más información, vea [Collation and Unicode Support](collation-and-unicode-support.md).  
  
-   Mediante el `Column.Collation` propiedad en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Objects (SMO).  
  
 No puede cambiar una intercalación de una columna a la que se hace referencia mediante uno de los siguientes elementos:  
  
-   Una columna calculada  
  
-   Un índice  
  
-   Estadísticas de distribución, ya sean generadas automáticamente o mediante la instrucción CREATE STATISTICS  
  
-   Una restricción CHECK  
  
-   Una restricción FOREIGN KEY  
  
 Al trabajar con la base de datos **tempdb**, la cláusula [COLLATE](/sql/t-sql/statements/collations) incluye una opción *database_default* para especificar que una columna de una tabla temporal use el valor predeterminado de intercalación de la base de datos del usuario actual para la conexión en lugar de la intercalación de **tempdb**.  
  
## <a name="collations-and-text-columns"></a>Intercalaciones y columnas de texto  
 Puede insertar o actualizar valores en una `text` columna cuya intercalación sea diferente de la página de códigos de la intercalación predeterminada de la base de datos. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] convierte implícitamente los valores a la intercalación de la columna.  
  
## <a name="collations-and-tempdb"></a>Intercalación y tempdb  
 La base de datos **tempdb** se crea cada vez que se inicia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y tiene la misma intercalación predeterminada que la base de datos **model** . Suele ser la misma que la intercalación predeterminada de la instancia. Si crea una base de datos de usuario y especifica una intercalación predeterminada distinta de **model**, la base de datos de usuario tiene una intercalación predeterminada distinta de **tempdb**. Todos los procedimientos almacenados temporales o tablas temporales se crean y se almacenan en **tempdb**. Esto significa que todas las columnas implícitas de las tablas temporales y todas las constantes, variables y parámetros coaccionable-predeterminados en los procedimientos almacenados temporales tienen intercalaciones distintas de los objetos comparables creados en las tablas y procedimientos almacenados permanentes.  
  
 Esto puede causar problemas con una discrepancia en intercalaciones entre bases de datos definidas por el usuario y objetos de base de datos del sistema. Por ejemplo, una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza la intercalación Latin1_General_CS_AS y se ejecutan las siguientes instrucciones:  
  
```  
CREATE DATABASE TestDB COLLATE Estonian_CS_AS;  
USE TestDB;  
CREATE TABLE TestPermTab (PrimaryKey int PRIMARY KEY, Col1 nchar );  
```  
  
 En este sistema, la base de datos **tempdb** usa la intercalación Latin1_General_CS_AS con la página de códigos 1252, y `TestDB` y `TestPermTab.Col1` usan la intercalación `Estonian_CS_AS` con la página de códigos 1257. Por ejemplo:  
  
```  
USE TestDB;  
GO  
-- Create a temporary table with the same column declarations  
-- as TestPermTab  
CREATE TABLE #TestTempTab (PrimaryKey int PRIMARY KEY, Col1 nchar );  
INSERT INTO #TestTempTab  
         SELECT * FROM TestPermTab;  
GO  
```  
  
 Con el ejemplo anterior, la base de datos **tempdb** usa la intercalación Latin1_General_CS_AS collation, y `TestDB` y `TestTab.Col1` usan la intercalación `Estonian_CS_AS` . Por ejemplo:  
  
```  
SELECT * FROM TestPermTab AS a INNER JOIN #TestTempTab on a.Col1 = #TestTempTab.Col1;  
```  
  
 Dado que **tempdb** usa la intercalación de servidor predeterminada y `TestPermTab.Col1` usa una intercalación diferente, SQL Server devuelve este error: "No se puede resolver el conflicto de intercalación entre 'Latin1_General_CI_AS_KS_WS' y 'Estonian_CS_AS' en la operación Igual a".  
  
 Para evitar el error, puede utilizar cualquiera de las alternativas siguientes:  
  
-   Especifique que la columna de la tabla temporal utilice la intercalación predeterminada de la base de datos de usuario, no **tempdb**. Esto permite que la tabla temporal trabaje con tablas de un formato parecido en varias bases de datos, si es un requisito de su sistema.  
  
    ```  
    CREATE TABLE #TestTempTab  
       (PrimaryKey int PRIMARY KEY,  
        Col1 nchar COLLATE database_default  
       );  
    ```  
  
-   Especifique la intercalación correcta de la columna `#TestTempTab` :  
  
    ```  
    CREATE TABLE #TestTempTab  
       (PrimaryKey int PRIMARY KEY,  
        Col1 nchar COLLATE Estonian_CS_AS  
       );  
    ```  
  
## <a name="see-also"></a>Vea también  
 [Configurar o cambiar la intercalación del servidor](set-or-change-the-server-collation.md)   
 [Establecer o cambiar la intercalación de base de datos](set-or-change-the-database-collation.md)   
 [Collation and Unicode Support](collation-and-unicode-support.md)  
  
  
