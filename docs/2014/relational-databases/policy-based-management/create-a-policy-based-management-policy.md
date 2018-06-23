---
title: Creación de una directiva de administración basada en directivas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Policy-Based Management, creating policies
ms.assetid: b28bf963-89f9-4941-b6c1-6004fec347f1
caps.latest.revision: 9
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 7c35a3c22fb025fdf4558e7c7324ec76368597c0
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36202013"
---
# <a name="create-a-policy-based-management-policy"></a>Crear una directiva de administración basada en directivas
  En este tema se describe cómo crear una directiva de administración basada en directivas en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para crear una directiva mediante:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 Requiere la pertenencia al rol PolicyAdministratorRole en la base de datos msdb.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-create-a-policy"></a>Para crear una directiva  
  
1.  En el **Explorador de objetos**, haga clic en el signo más para expandir el servidor en el que quiere crear una directiva de administración basada en directivas.  
  
2.  Haga clic en el signo más para expandir la carpeta **Administración** .  
  
3.  Haga clic en el signo más para expandir la carpeta **Administración de directivas**.  
  
4.  Haga clic con el botón derecho en la carpeta **Directivas** y, después, seleccione **Nueva directiva**.  
  
5.  En el cuadro de diálogo **Crear nueva directiva** , en el cuadro **Nombre** , escriba el nombre de la nueva directiva.  
  
6.  Si desea que la directiva se habilite en cuanto se cree, active la casilla **Habilitado** . Si el modo de evaluación es **A petición**, la casilla **Habilitado** no está disponible.  
  
7.  En la lista **Condición de comprobación** , seleccione una de las condiciones existentes o seleccione **Nueva condición**. Para modificar una condición, selecciónela y, después, haga clic en los puntos suspensivos (**...**). Para obtener más información, vea [Crear una nueva condición de administración basada en directivas.](create-a-new-policy-based-management-condition.md) o [Ver o modificar las propiedades de una condición de administración basada en directivas](view-or-modify-the-properties-of-a-policy-based-management-condition.md).  
  
8.  En el cuadro **Para destinos** , seleccione uno o varios tipos de destino para esta directiva. Algunas condiciones y facetas solo se pueden aplicar a ciertos tipos de destinos. Los conjuntos de destinos disponibles aparecen en el cuadro asociado. Expanda **Cada** para seleccionar una condición de filtrado para algunos tipos de destinos. Si en este cuadro no aparece ningún destino, la condición de comprobación se investiga en el nivel de servidor.  
  
9. En el cuadro **Modo de evaluación** , seleccione cómo se comportará esta directiva. Condiciones diferentes pueden tener distintos modos de evaluación válidos. Para obtener más información sobre los modos de evaluación válidos, vea [Administrar servidores mediante administración basada en directivas](administer-servers-by-using-policy-based-management.md).  
  
10. Si la directiva se va a evaluar según una programación, establezca el modo de evaluación en **Al programar**y, a continuación, haga clic en **Seleccionar** para seleccionar una programación o haga clic en **Nuevo** para crear una nueva programación.  
  
11. Para limitar la directiva al subconjunto de los tipos de destino, en el cuadro **Restricción de servidor** , seleccione las condiciones de limitación o cree una condición nueva.  
  
     Para obtener más información acerca de las opciones disponibles en el cuadro de diálogo **Crear nueva directiva** , vea [Cuadro de diálogo Crear nueva directiva o Abrir directiva, página General](../../integration-services/general-page-of-integration-services-designers-options.md) o [Cuadro de diálogo Crear nueva directiva o Abrir directiva, página Descripción](create-new-policy-or-open-policy-dialog-box-description-page.md).  
  
12. Cuando termine, haga clic en **Aceptar**.  
  
  