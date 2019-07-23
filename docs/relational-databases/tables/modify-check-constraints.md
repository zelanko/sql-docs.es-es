---
title: Modificación de restricciones CHECK | Microsoft Docs
ms.custom: ''
ms.date: 06/28/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- CHECK constraints, modifying
- modifying constraints
- constraints [SQL Server], check
- constraints [SQL Server], modifying
ms.assetid: f22daef8-e350-40ef-8ff0-b5f87d1d9e56
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 35ab525e1420d5e8db2a63f4892d8e17a3673158
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68139617"
---
# <a name="modify-check-constraints"></a>Modificar restricciones CHECK
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Puede modificar una restricción CHECK en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)] si desea cambiar la expresión de la restricción o las opciones que habilitan o deshabilitan la restricción para condiciones específicas.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para modificar una restricción CHECK con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Requiere el permiso ALTER en la tabla.  
  
##  <a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
  
#### <a name="to-modify-a-check-constraint"></a>Para modificar una restricción CHECK  
  
1.  En el **Explorador de objetos**, haga clic con el botón derecho en la tabla que contiene la restricción CHECK y seleccione **Diseñar**.  
  
2.  En el menú **Diseñador de tablas**, haga clic en **Restricciones CHECK...** .  
  
3.  En el cuadro de diálogo **Restricciones CHECK** , en **Restricción CHECK seleccionada**, seleccione la restricción que desee modificar.  
  
4.  Complete una de las acciones descritas en la tabla siguiente:  
  
    |A|Siga estos pasos|  
    |--------|------------------------|  
    |Modificar la expresión de restricción|Escriba la nueva expresión en el campo **Expresión** .|  
    |Cambiar el nombre de la restricción|Escriba un nuevo nombre en el campo **Nombre** .|  
    |Aplicar la restricción a datos existentes|Active la opción **Comprobar datos existentes al crear o habilitar** .|  
    |Deshabilitar la restricción cuando se agregan nuevos datos a la tabla o cuando se actualizan datos existentes en la tabla.|Desactive la opción **Exigir restricción para INSERT y UPDATE** .|  
    |Deshabilitar la restricción cuando un agente de replicación inserta o actualiza datos en una tabla.|Desactive la opción **Exigir para replicación** .|  
  
    > [!NOTE]  
    >  Algunas bases de datos tienen diferente funcionalidad para las restricciones CHECK.  
  
5.  Haga clic en **Cerrar**.  
  
6.  En el menú **Archivo** , haga clic en **Guardar**_table name_.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 **Para modificar una restricción CHECK**  
  
 Para modificar una restricción `CHECK` mediante [!INCLUDE[tsql](../../includes/tsql-md.md)], primero deberá eliminar la restricción `CHECK` existente y, a continuación, volver a crearla con la nueva definición. Para obtener más información, vea [Eliminar restricciones CHECK](../../relational-databases/tables/delete-check-constraints.md) y [Crear restricciones CHECK](../../relational-databases/tables/create-check-constraints.md).  
  
###  <a name="TsqlExample"></a>  
