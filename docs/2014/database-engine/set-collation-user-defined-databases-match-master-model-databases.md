---
title: Establecer las bases de datos definido por el usuario de intercalación coinciden con los del patrón y bases de datos modelo | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: c686446f-dae1-4b05-a3df-837b3422988d
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: dfb00b1cc1a9930f7a374403b40e2c0d793eb090
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62773321"
---
# <a name="set-the-collation-of-user-defined-databases-to-match-those-of-the-master-and-model-databases"></a>Establecer la intercalación de bases de datos definidas por el usuario para que coincidan con las de las bases de datos modelo y maestra
  Esta regla comprueba si las bases de datos definidas por el usuario se definen utilizando una intercalación de base de datos que es igual a la intercalación de las bases de datos maestra o modelo.  
  
## <a name="best-practices-recommendations"></a>Prácticas recomendadas  
 Recomendamos que las intercalaciones de bases de datos definidas por el usuario coincidan con la intercalación de las bases de datos maestra o modelo. De lo contrario, pueden producirse conflictos de intercalación que podrían impedir que el código se ejecute. Por ejemplo, cuando un procedimiento almacenado une una tabla a una tabla temporal, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] podría finalizar el lote y devolver un error de conflicto de intercalación si las intercalaciones de la base de datos definida por el usuario y la base de datos modelo son diferentes. Esto se debe a que las tablas temporales se crean en tempdb, que basa su intercalación en la de la base de datos modelo.  
  
 Si experimenta errores de conflictos de intercalación, considere una de las soluciones siguientes:  
  
-   Exporte los datos de la base de datos de usuario e impórtelos en tablas nuevas que tengan la misma intercalación que las bases de datos modelo y maestra.  
  
-   Vuelva a generar las bases de datos del sistema para utilizar una intercalación que coincida con la intercalación de las bases de datos de usuario. Para obtener más información acerca de cómo volver a generar las bases de datos del sistema, consulte [volver a generar las bases de datos del sistema](../relational-databases/databases/system-databases.md).  
  
-   Modifique cualquier procedimiento almacenado que una las tablas de usuario a las tablas en tempdb para crear las tablas en tempdb utilizando la intercalación de la base de datos de usuario. Para ello, agregue la cláusula `COLLATE database_default` a las definiciones de columna de la tabla temporal, como se muestra en el ejemplo siguiente:  
  
    ```  
    CREATE TABLE #temp1 ( c1 int, c2 varchar(30) COLLATE database_default )  
    ```  
  
## <a name="for-more-information"></a>Para obtener más información  
 [Establecer o cambiar la intercalación de base de datos](../relational-databases/collations/set-or-change-the-database-collation.md)  
  
 [Establecer o cambiar la intercalación de columnas](../relational-databases/collations/set-or-change-the-column-collation.md)  
  
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)  
  
 [COLLATE &#40;Transact-SQL&#41;](/sql/t-sql/statements/collations)  
  
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)  
  
 [Artículo de Microsoft Knowledge Base 325335](https://go.microsoft.com/fwlink/?linkid=117751)  
  
 [Cómo: Instalar a SQL Server 2008 desde el símbolo del sistema](https://go.microsoft.com/fwlink/?LinkId=81585)  
  
## <a name="see-also"></a>Vea también  
 [Supervisar y aplicar las prácticas recomendadas usando la administración basada en directivas](../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
