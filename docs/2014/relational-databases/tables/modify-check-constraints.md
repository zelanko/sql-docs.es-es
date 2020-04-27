---
title: Modificación de restricciones CHECK | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 651b13121653f5627f59bc6a8a11f1e2e49c43b2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "68211840"
---
# <a name="modify-check-constraints"></a>Modificar restricciones CHECK
  Puede modificar una restricción CHECK en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)] si desea cambiar la expresión de la restricción o las opciones que habilitan o deshabilitan la restricción para condiciones específicas.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para modificar una restricción CHECK con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="security"></a><a name="Security"></a> Seguridad  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permisos  
 Requiere el permiso ALTER en la tabla.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
  
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
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usar Transact-SQL  
 **Para modificar una restricción CHECK**  
  
 Para modificar una restricción `CHECK` mediante [!INCLUDE[tsql](../../includes/tsql-md.md)], primero deberá eliminar la restricción `CHECK` existente y, a continuación, volver a crearla con la nueva definición. Para obtener más información, vea [Eliminar restricciones CHECK](delete-check-constraints.md) y [Crear restricciones CHECK](create-check-constraints.md).  
  
###  <a name="TsqlExample"></a>  
