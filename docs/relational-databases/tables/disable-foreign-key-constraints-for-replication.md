---
title: Deshabilitar una restricción FOREIGN KEY para la replicación | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: table-view-index, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: table-view-index
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- constraints [SQL Server], foreign keys
- foreign keys [SQL Server], disabling constraints
- disabling constraints
ms.assetid: 4211f2fd-d16a-4081-995c-43f1f0827f0b
caps.latest.revision: 20
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 342e975b72e338157794566966e8676a65217bad
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43074311"
---
# <a name="disable-foreign-key-constraints-for-replication"></a>Deshabilitar una restricción FOREIGN KEY para la replicación
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  Puede deshabilitar las restricciones de clave externa para la replicación en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Esto puede ser útil si se publican datos de una versión anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Si se publica la tabla mediante replicación, se deshabilitan automáticamente las restricciones FOREIGN KEY para las operaciones realizadas por los agentes de replicación. Cuando un agente de replicación realiza una inserción, actualización o eliminación en un suscriptor, no se comprueba la restricción. En cambio, sí se comprueba cuando lo hace un usuario. La restricción se deshabilitará para el agente de replicación porque ya se comprobó en el publicador cuando se insertaron, actualizaron o eliminaron los datos originalmente.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para deshabilitar una restricción de clave externa para la replicación, use:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 Requiere el permiso ALTER en la tabla.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-disable-a-foreign-key-constraint-for-replication"></a>Para deshabilitar una restricción FOREIGN KEY para la replicación  
  
1.  En el **Explorador de objetos**, expanda la tabla con la restricción de clave externa que desee modificar y, a continuación, expanda la carpeta **Claves** .  
  
2.  Haga clic con el botón derecho en la restricción de clave externa y, luego, haga clic en **Modificar**.  
  
3.  En el cuadro de diálogo **Relaciones de clave externa** , seleccione el valor **No** para **Exigir para replicación**.  
  
4.  Haga clic en **Cerrar**.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-disable-a-foreign-key-constraint-for-replication"></a>Para deshabilitar una restricción FOREIGN KEY para la replicación  
  
1.  Para realizar esta tarea en [!INCLUDE[tsql](../../includes/tsql-md.md)], quite la restricción de clave externa. Después agregue una nueva restricción de clave externa y especifique la opción NOT FOR REPLICATION.  
  
 Para obtener más información, vea [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md).  
  
###  <a name="TsqlExample"></a>  
