---
title: Implementar desencadenadores DDL | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-ddl
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- DDL triggers, implementing
ms.assetid: f44e5340-1d18-40e9-828e-0ffcca091ae3
caps.latest.revision: 31
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: b1264082262e616722b88d9a3a80b509aec4fc5c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36114213"
---
# <a name="implement-ddl-triggers"></a>Implementar desencadenadores DDL
  En este tema se ofrece información acerca de la creación y modificación de desencadenadores DDL, así como para su deshabilitación o eliminación.  
  
## <a name="creating-ddl-triggers"></a>Crear desencadenadores DDL  
 Los desencadenadores DDL se crean con la instrucción CREATE TRIGGER de [!INCLUDE[tsql](../../includes/tsql-md.md)] para desencadenadores DDL.  
  
 **Para crear un desencadenador DDL**  
  
-   [CREATE TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-trigger-transact-sql)  
  
> [!IMPORTANT]  
>  La capacidad de devolver conjuntos de resultados desde desencadenadores se eliminará en una versión posterior de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Los desencadenadores que devuelven conjuntos de resultados pueden provocar un comportamiento inesperado en aplicaciones que no estén diseñadas para utilizarlos. Evite la devolución de conjuntos de resultados desde desencadenadores en los nuevos trabajos de desarrollo y piense en modificar las aplicaciones que la usan actualmente. Para evitar que los desencadenadores devuelvan conjuntos de resultados en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], establezca la opción [disallow results from triggers](../../database-engine/configure-windows/disallow-results-from-triggers-server-configuration-option.md) en 1. El valor predeterminado de esta opción será 1 en una versión futura de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="modifying-ddl-triggers"></a>Modificar desencadenadores DDL  
 Si necesita modificar la definición de un desencadenador DDL, puede quitarlo y volver a crearlo, o bien volver a definirlo en un solo paso.  
  
 Si cambia el nombre de un objeto al que hace referencia un desencadenador DDL, debe modificar el desencadenador para que el texto refleje el nuevo nombre. Por lo tanto, antes de cambiar el nombre de un objeto, vea primero las dependencias del mismo para determinar si algún desencadenador va a verse afectado por el cambio propuesto.  
  
 También es posible modificar un desencadenador para cifrar su definición.  
  
 **Para modificar un desencadenador**  
  
-   [ALTER TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-trigger-transact-sql)  
  
 **Para ver las dependencias de un desencadenador**  
  
-   [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql)  
  
-   [sys.dm_sql_referenced_entities &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql)  
  
-   [sys.dm_sql_referencing_entities &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql)  
  
## <a name="disabling-and-dropping-ddl-triggers"></a>Deshabilitar y quitar desencadenadores DDL  
 Puede eliminar o deshabilitar un desencadenador DDL cuando ya no lo necesite.  
  
 Al deshabilitar un desencadenador DDL, éste no se quita. Sigue siendo un objeto de la base de datos actual. Sin embargo, el desencadenador no se activa cuando se ejecuta una instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] en la que se programó. Los desencadenadores DDL deshabilitados se pueden volver a habilitar. La habilitación de un desencadenador DDL hace que se active tal como lo hizo cuando se creó originalmente. Cuando se crean desencadenadores DDL, se habilitan de forma predeterminada.  
  
 Cuando el desencadenador DDL se elimina, se quita de la base de datos actual. Los objetos o datos incluidos en el ámbito del desencadenador DDL no se ven afectados.  
  
 **Para deshabilitar un desencadenador DDL**  
  
-   [DISABLE TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/disable-trigger-transact-sql)  
  
-   [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql)  
  
 **Para habilitar un desencadenador DDL**  
  
-   [ENABLE TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/enable-trigger-transact-sql)  
  
-   [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql)  
  
 **Para eliminar un desencadenador DDL**  
  
-   [DROP TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-trigger-transact-sql)  
  
  
