---
title: Modificación de estadísticas | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- statistics [SQL Server], modifying
- modifying statistics
ms.assetid: b06299ca-ed52-411a-b245-45eac4628c99
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 593a30631eed27db108c79dd70840d1fee3f6964
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68134013"
---
# <a name="modify-statistics"></a>Modificar estadísticas
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
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
  
7.  Haga clic en **Aceptar**.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 **Para modificar las estadísticas**  
  
 Esta tarea no se puede realizar mediante instrucciones Transact-SQL. Para modificar las estadísticas con Transact-SQL, primero debe eliminar la estadística existente y, a continuación, volver a crearla con nuevos atributos.  
  
 Para obtener más información, vea [DROP STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/drop-statistics-transact-sql.md) y [CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md).  
  
  
