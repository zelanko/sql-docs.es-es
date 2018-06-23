---
title: Ver o modificar las propiedades de una directiva de administración basada en directivas | Microsoft Docs
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
- Policy-Based Management, modify policies
- Policy-Based Management, view policies
ms.assetid: ba805504-5db5-4731-a8da-a0e89cb20c37
caps.latest.revision: 8
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: b64630b7a586eb8b32f225110da026656cdc4325
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36197911"
---
# <a name="view-or-modify-the-properties-of-a-policy-based-management-policy"></a>Ver o modificar las propiedades de una directiva de administración basada en directivas
  En este tema se describe cómo ver o modificar las propiedades de una directiva de administración basada en directivas en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para ver o modificar las propiedades de una directiva mediante:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 Requiere la pertenencia al rol PolicyAdministratorRole en la base de datos msdb.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-view-the-properties-of-all-policies-on-an-object"></a>Para ver las propiedades de todas las directivas de un objeto  
  
1.  En el Explorador de objetos, haga clic con el botón derecho en un servidor, objeto de servidor, base de datos u objeto de base de datos, elija **Directivas** y seleccione **Ver**. Para obtener más información sobre las opciones disponibles en el cuadro de diálogo **Ver directivas –***nombre_de_objeto*, vea [Cuadro de diálogo Ver directivas](view-policies-dialog-box.md).  
  
2.  Cuando termine, haga clic en **Cerrar**.  
  
#### <a name="to-view-or-modify-a-specific-policys-properties"></a>Para ver o modificar las propiedades de una directiva específica  
  
1.  En el **Explorador de objetos**, haga clic en el signo más para expandir el servidor que contiene la directiva de administración basada en directivas que quiera ver o modificar.  
  
2.  Haga clic en el signo más para expandir la carpeta **Administración** .  
  
3.  Haga clic en el signo más para expandir la carpeta **Administración de directivas**.  
  
4.  Haga clic en el signo más para expandir la carpeta **Directivas** .  
  
5.  Haga clic con el botón derecho en la directiva que quiera ver o editar y seleccione **Propiedades**. Para obtener más información sobre las opciones disponibles en el cuadro de diálogo *Abrir directiva –***nombre_de_directiva*, vea [Cuadro de diálogo Crear nueva directiva o Abrir directiva, página General](../../integration-services/general-page-of-integration-services-designers-options.md) y [Cuadro de diálogo Crear nueva directiva o Abrir directiva, página Descripción](create-new-policy-or-open-policy-dialog-box-description-page.md).  
  
6.  Cuando termine, haga clic en **Aceptar**.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-view-a-policys-properties"></a>Para ver las propiedades de una directiva  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    USE msdb;  
    GO  
    SELECT name,  
       execution_mode,  
       description,  
       is_enabled,  
       job_id  
    FROM syspolicy_policies;  
    GO  
    ```  
  
 Para obtener más información, vea [syspolicy_policies &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/syspolicy-policies-transact-sql).  
  
  
