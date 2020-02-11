---
title: Modificación de estadísticas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- statistics [SQL Server], modifying
- modifying statistics
ms.assetid: b06299ca-ed52-411a-b245-45eac4628c99
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 2da978efd869a748bb48f6d494d59ae2f4cfb019
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68211861"
---
# <a name="modify-statistics"></a>Modificar estadísticas
  En [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , puede modificar las estadísticas existentes mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para modificar las estadísticas, use:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Requiere que:  
  
-   El usuario tiene el permiso ALTER en la tabla o la vista.  
  
-   El usuario debe ser el propietario de la tabla o vista indexada o un miembro de uno de los roles siguientes: rol fijo de servidor **sysadmin** , rol fijo de base de datos **db_owner** o rol fijo de base de datos **db_ddladmin** .  
  
##  <a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
  
#### <a name="to-modify-statistics"></a>Para modificar las estadísticas  
  
1.  En el **Explorador de objetos**, haga clic en el signo más para expandir la base de datos en la que desea modificar una estadística.  
  
2.  Haga clic en el signo más para expandir la carpeta **Tablas** .  
  
3.  Haga clic en el signo más para expandir la tabla en la que desea modificar una estadística.  
  
4.  Haga clic en el signo más para expandir la carpeta **Estadísticas** .  
  
5.  Haga clic con el botón derecho en el objeto de estadísticas que quiera modificar y seleccione **Propiedades**.  
  
6.  En el cuadro de diálogo **Propiedades de estadísticas:** *nombre_estadísticas*, en la página **General**, haga clic en **Agregar**, **Quitar**, **Subir**o **Bajar**o cualquier combinación, para alterar las propiedades de las estadísticas. Recuerde que la ubicación de una columna dentro de la cuadrícula **Columnas de estadísticas** puede afectar considerablemente a la utilidad de las estadísticas.  
  
7.  Haga clic en **OK**.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 **Para modificar las estadísticas**  
  
 Esta tarea no se puede realizar mediante instrucciones Transact-SQL. Para modificar las estadísticas con Transact-SQL, primero debe eliminar la estadística existente y, a continuación, volver a crearla con nuevos atributos.  
  
 Para obtener más información, vea [DROP STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-statistics-transact-sql) y [CREATE STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-statistics-transact-sql).  
  
  
