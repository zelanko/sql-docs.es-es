---
title: "Creación y administración de catálogos de texto completo | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: search
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-search
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- full-text catalogs [SQL Server], creating
- full-text search [SQL Server], using SQL Server Management Studio
ms.assetid: 824b7131-44a6-4815-89e6-62b7bab060e3
caps.latest.revision: "21"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 82eda03e726cc16476847cc8ed21ad46f77509cb
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/02/2018
---
# <a name="create-and-manage-full-text-catalogs"></a>Crear y administrar catálogos de texto completo
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)] Un catálogo de texto completo es un contenedor lógico para un grupo de índices de texto completo. Tendrá que crear un catálogo de texto completo antes de poder crear un índice de texto completo.

Un catálogo de texto completo es un objeto virtual y no pertenece a ningún grupo de archivos.
  
##  <a name="creating"></a> Crear un catálogo de texto completo  

### <a name="create-a-full-text-catalog-with-transact-sql"></a>Crear un catálogo de texto completo con Transact-SQL
Use [CREATE FULLTEXT CATALOG](../../t-sql/statements/create-fulltext-catalog-transact-sql.md). Por ejemplo:

```sql 
USE AdventureWorks;  
GO  
CREATE FULLTEXT CATALOG ftCatalog AS DEFAULT;  
GO  
``` 

### <a name="create-a-full-text-catalog-with-management-studio"></a>Crear un catálogo de texto completo con Management Studio
1.  En el Explorador de objetos, expanda el servidor, expanda **Bases de datos**y, después, expanda la base de datos en la que quiere crear el catálogo de texto completo.  
  
2.  Expanda **Almacenamiento**y, después, haga clic con el botón derecho en **Catálogos de texto completo**.  
  
3.  Seleccione **Nuevo catálogo de texto completo**.  
  
4.  En el cuadro de diálogo **Nuevo catálogo de texto completo**, especifique la información del catálogo que va a volver a crear. Para obtener más información, vea [Búsqueda de texto completo](http://msdn.microsoft.com/library/5ed6f7cd-d9af-4439-9f33-fc935b883d91).  
  
    > [!NOTE]  
    >  Los identificadores de los catálogos de texto completo comienzan por 00005 y se incrementan en uno con cada nuevo catálogo que se crea.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="props"></a> Obtener las propiedades de un catálogo de texto completo  
Use la función de [!INCLUDE[tsql](../../includes/tsql-md.md)] **FULLTEXTCATALOGPROPERTY** para obtener el valor de diversas propiedades relacionadas con los catálogos de texto completo. Para obtener más información, consulte [FULLTEXTCATALOGPROPERTY](../../t-sql/functions/fulltextcatalogproperty-transact-sql.md).

Por ejemplo, ejecute la siguiente consulta para obtener el recuento de índices en el catálogo de texto completo `Catalog1`.

```sql 
USE <database>;  
GO  
SELECT fulltextcatalogproperty('Catalog1', 'ItemCount');  
GO  
```  
  
En la siguiente tabla se muestran las propiedades relacionadas con los catálogos de texto completo. Esta información puede ser útil para administrar y solucionar problemas de la búsqueda de texto completo. 
  
|Propiedad|Description|  
|--------------|-----------------|  
|**AccentSensitivity**|Opción de distinción de acentos.|
|**ImportStatus**|Si se va a importar el catálogo de texto completo.|  
|**IndexSize**|Tamaño, en megabytes (MB), del catálogo de texto completo.| 
|**ItemCount**|Número de elementos de texto completo indizados que contiene actualmente el catálogo de texto completo.|  
|**MergeStatus**|Si hay una combinación maestra en curso.| 
|**PopulateCompletionAge**|Diferencia, en segundos, entre la terminación del último rellenado del índice de texto completo y 01/01/1990 00:00:00.| 
|**PopulateStatus**|Estado del rellenado.<br /><br /> [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]|  
|**UniqueKeyCount**|Número de claves únicas en el catálogo de texto completo.| 

##  <a name="rebuildone"></a> Regenerar un catálogo de texto completo  

Ejecute la instrucción de Transact-SQL [ALTER FULLTEXT CATALOG... REBUILD](
../../t-sql/statements/alter-fulltext-catalog-transact-sql.md) o realice las siguientes tareas en SQL Server Management Studio (SSMS).

1.  En SSMS, en el Explorador de objetos, expanda el servidor, expanda **Bases de datos**y, después, expanda la base de datos que contiene el catálogo de texto completo que quiere volver a generar.  
  
2.  Expanda **Almacenamiento**y, a continuación, expanda **Catálogos de texto completo**.  
  
3.  Haga clic con el botón derecho en el nombre del catálogo de texto completo que quiere volver a generar y seleccione **Volver a generar**.  
  
4.  Ante la pregunta **¿Quiere eliminar el catálogo de texto completo y volver a generarlo?**, haga clic en **Aceptar**.  
  
5.  En el cuadro de diálogo **Volver a generar el catálogo de texto completo** , haga clic en **Cerrar**.  
   
##  <a name="rebuildall"></a> Recompilar todos los catálogos de texto completo para una base de datos  

1.  En SSMS, en el Explorador de objetos, expanda el servidor, expanda **Bases de datos**y, después, expanda la base de datos que contiene los catálogos de texto completo que quiere volver a generar.  
  
2.  Expanda **Almacenamiento**y, después, haga clic con el botón derecho en **Catálogos de texto completo**.  
  
3.  Seleccione **Volver a generar todo**.  
  
4.  Ante la pregunta **¿Quiere eliminar todos los catálogos de texto completo y volver a generarlos?**, haga clic en **Aceptar**.  
  
5.  En el cuadro de diálogo **Volver a generar todos los catálogos de texto completo** , haga clic en **Cerrar**.  
  
  
  
##  <a name="removing"></a> Quitar un catálogo de texto completo de una base de datos  

Ejecute la instrucción de Transact-SQL [DROP FULLTEXT CATALOG](
../../t-sql/statements/drop-fulltext-catalog-transact-sql.md) o realice las siguientes acciones en SQL Server Management Studio (SSMS).

1.  En SSMS, en el Explorador de objetos, expanda el servidor, expanda **Bases de datos**y expanda la base de datos que contiene el catálogo de texto completo que quiere quitar.  
  
2.  Expanda **Almacenamiento**y, a continuación, **Catálogos de texto completo**.  
  
3.  Haga clic con el botón derecho en el catálogo de texto completo que quiere quitar y seleccione **Eliminar**.  
  
4.  En el cuadro de diálogo **Eliminar objetos** , haga clic en **Aceptar**.  

## <a name="next-step"></a>Paso siguiente
[Crear y administrar índices de texto completo](../../relational-databases/search/create-and-manage-full-text-indexes.md)
