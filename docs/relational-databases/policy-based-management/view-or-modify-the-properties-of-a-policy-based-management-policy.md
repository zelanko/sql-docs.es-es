---
title: "Ver o modificar las propiedades de una directiva de administraci&#243;n basada en directivas | Microsoft Docs"
ms.custom: ""
ms.date: "10/06/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Administración basada en directivas, modificar directivas"
  - "Administración basada en directivas, ver directivas"
ms.assetid: ba805504-5db5-4731-a8da-a0e89cb20c37
caps.latest.revision: 9
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 9
---
# Ver o modificar las propiedades de una directiva de administraci&#243;n basada en directivas
  En este tema se describe cómo ver o modificar las propiedades de una directiva de administración basada en directivas en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
  
####  <a name="Permissions"></a> Permissions  
 Requiere la pertenencia al rol PolicyAdministratorRole en la base de datos msdb.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### Para ver las propiedades de todas las directivas de un objeto  
  
1.  En el Explorador de objetos, haga clic con el botón derecho en un servidor, objeto de servidor, base de datos u objeto de base de datos, elija **Directivas** y seleccione **Ver**. Para obtener más información sobre las opciones disponibles en el cuadro de diálogo **Ver directivas - ***nombre_objeto*, vea [Cuadro de diálogo Ver directivas](../../relational-databases/policy-based-management/view-policies-dialog-box.md).  
  
2.  Cuando termine, haga clic en **Cerrar**.  
  
#### Para ver o modificar las propiedades de una directiva específica  
  
1.  En el **Explorador de objetos**, haga clic en el signo más para expandir el servidor que contiene la directiva de administración basada en directivas que quiera ver o modificar.  
  
2.  Haga clic en el signo más para expandir la carpeta **Administración** .  
  
3.  Haga clic en el signo más para expandir la carpeta **Administración de directivas**.  
  
4.  Haga clic en el signo más para expandir la carpeta **Directivas** .  
  
5.  Haga clic con el botón derecho en la directiva que quiera ver o editar y seleccione **Propiedades**. Para obtener más información sobre las opciones disponibles en el cuadro de diálogo **Abrir directiva –***nombre_directiva*, vea [Cuadro de diálogo Crear nueva directiva o Abrir directiva, página General](../../relational-databases/policy-based-management/create-new-policy-or-open-policy-dialog-box-general-page.md) y [Cuadro de diálogo Crear nueva directiva o Abrir directiva, página Descripción](../../relational-databases/policy-based-management/create-new-policy-or-open-policy-dialog-box-description-page.md).  
  
6.  Cuando termine, haga clic en **Aceptar**.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### Para ver las propiedades de una directiva  
  
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
  
 Para obtener más información, vea [syspolicy_policies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syspolicy-policies-transact-sql.md).  
  
  