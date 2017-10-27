---
title: "Modificación de restricciones CHECK | Microsoft Docs"
ms.custom: 
ms.date: 06/28/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- CHECK constraints, modifying
- modifying constraints
- constraints [SQL Server], check
- constraints [SQL Server], modifying
ms.assetid: f22daef8-e350-40ef-8ff0-b5f87d1d9e56
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 56805de308b7824cbfb948de432131c139db9df0
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

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
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-modify-a-check-constraint"></a>Para modificar una restricción CHECK  
  
1.  En el **Explorador de objetos**, haga clic con el botón derecho en la tabla que contiene la restricción CHECK y seleccione **Diseñar**.  
  
2.  En el menú **Diseñador de tablas** , haga clic en **Restricciones CHECK**.  
  
3.  En el cuadro de diálogo **Restricciones CHECK** , en **Restricción CHECK seleccionada**, seleccione la restricción que desee modificar.  
  
4.  Complete una de las acciones descritas en la tabla siguiente:  
  
    |Para|Siga estos pasos|  
    |--------|------------------------|  
    |Modificar la expresión de restricción|Escriba la nueva expresión en el campo **Expresión** .|  
    |Cambiar el nombre de la restricción|Escriba un nuevo nombre en el campo **Nombre** .|  
    |Aplicar la restricción a datos existentes|Active la opción **Comprobar datos existentes al crear o habilitar** .|  
    |Deshabilitar la restricción cuando se agregan nuevos datos a la tabla o cuando se actualizan datos existentes en la tabla.|Desactive la opción **Exigir restricción para INSERT y UPDATE** .|  
    |Deshabilitar la restricción cuando un agente de replicación inserta o actualiza datos en una tabla.|Desactive la opción **Exigir para replicación** .|  
  
    > [!NOTE]  
    >  Algunas bases de datos tienen diferente funcionalidad para las restricciones CHECK.  
  
5.  Haga clic en **Cerrar**.  
  
6.  En el menú **Archivo** , haga clic en **Guardar***table name*.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 **Para modificar una restricción CHECK**  
  
 Para modificar una restricción `CHECK` mediante [!INCLUDE[tsql](../../includes/tsql-md.md)], primero deberá eliminar la restricción `CHECK` existente y, a continuación, volver a crearla con la nueva definición. Para obtener más información, vea [Eliminar restricciones CHECK](../../relational-databases/tables/delete-check-constraints.md) y [Crear restricciones CHECK](../../relational-databases/tables/create-check-constraints.md).  
  
###  <a name="TsqlExample"></a>  

