---
title: Creación de una nueva condición de administración basada en directivas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, creating policy conditions
ms.assetid: 8a612f7e-6c70-49db-a4de-48431e097cc5
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 942a0be0503cd728defb6800a516b0cb0c85c13f
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52804297"
---
# <a name="create-a-new-policy-based-management-condition"></a>Crear una nueva condición de administración basada en directivas.
  En este tema se describe cómo crear una condición de administración basada en directivas en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para crear una condición mediante:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 Requiere la pertenencia al rol PolicyAdministratorRole en la base de datos msdb.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-create-a-condition"></a>Para crear una condición  
  
1.  En el **Explorador de objetos**, haga clic en el signo más para expandir el servidor en el que quiera crear una condición de administración basada en directivas.  
  
2.  Haga clic en el signo más para expandir la carpeta **Administración** .  
  
3.  Haga clic en el signo más para expandir la carpeta **Administración de directivas**.  
  
4.  Haga clic en el signo más para expandir la carpeta **Facetas** .  
  
5.  Haga clic con el botón derecho en la faceta en la que quiere crear una nueva condición y seleccione **Nueva condición**.  
  
6.  En el cuadro de diálogo **Crear nueva condición** , en el cuadro **Nombre** , escriba el nombre de la nueva condición.  
  
7.  Confirme que la faceta es correcta en la lista **Faceta** o seleccione una faceta diferente.  
  
8.  En **Expresión**, construya las expresiones de condiciones seleccionando una propiedad de faceta en el cuadro **Campo** , junto con su operador y valor asociados. Si agrega varias expresiones, estas pueden combinarse con **Y** u **O**. Para obtener más información sobre las opciones disponibles en este cuadro de diálogo, vea [Cuadro de diálogo Crear nueva condición o Abrir condición, página General](../../integration-services/general-page-of-integration-services-designers-options.md), [Cuadro de diálogo Crear nueva condición o Abrir condición, página Descripción](create-new-condition-or-open-condition-dialog-box-description-page.md) y [Cuadro de diálogo Edición avanzada &#40;condición&#41;](advanced-edit-condition-dialog-box.md).  
  
9. Cuando termine, haga clic en **Aceptar**.  
  
  
