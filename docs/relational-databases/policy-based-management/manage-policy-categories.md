---
title: "Administrar categor&#237;as de directiva | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.swb.dmf.policycategories.f1"
ms.assetid: d188a819-731f-4029-98aa-780d3299a0ce
caps.latest.revision: 18
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 18
---
# Administrar categor&#237;as de directiva
  En este tema se describe cómo se aplica una o todas las directivas disponibles en una categoría a toda la instancia de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   **Para aplicar directivas de categoría a una instancia de SQL Server con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   Cuando se usa [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], si la casilla **Suscripciones de base de datos de mandatos** no está activada, la categoría de directiva debe aplicarse individualmente a cada parte correspondiente del servidor, por ejemplo, a una o varias bases de datos o tablas.  
  
-   Si especifica una categoría de directiva que no existe, se crea una categoría de directiva nueva y la suscripción se asigna para todas las bases de datos al ejecutar el procedimiento almacenado. Si luego borra la suscripción asignada para la nueva categoría, la suscripción solo se aplicará para la base de datos que especificó como *target_object*. Para obtener más información sobre cómo cambiar una configuración de suscripción asignada, vea [sp_syspolicy_update_policy_category &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-update-policy-category-transact-sql.md).  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Este procedimiento almacenado se ejecuta en el contexto del propietario actual del procedimiento almacenado.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### Para aplicar directivas de categoría a una instancia de SQL Server  
  
1.  En el **Explorador de objetos**, haga clic en el signo más para expandir el servidor en el que aplicará las directivas de categoría.  
  
2.  Haga clic en el signo más para expandir la carpeta **Administración** .  
  
3.  Haga clic con el botón derecho en **Administración de directivas** y seleccione **Administrar categorías**.  
  
     La siguiente información está disponible en el cuadro de diálogo **Administrar categorías de directiva** :  
  
     **Nombre**  
     Nombre de la categoría de directiva.  
  
     **Suscripciones de base de datos de mandatos**  
     Obliga a que todas las bases de datos de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] exijan directivas en la categoría de directiva.  
  
4.  Active o desactive alguna o todas las casillas situadas bajo **Suscripciones de base de datos de mandatos** para aplicar esa categoría de directiva a la instancia de SQL Server.  
  
5.  Cuando termine, haga clic en **Aceptar**.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### Para aplicar directivas de categoría a una instancia de SQL Server  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    USE msdb;  
    GO  
    -- configures the specified database to subscribe to a policy category that is named 'Table Naming Policies'.  
    EXEC dbo.sp_syspolicy_add_policy_category_subscription @target_type = N'DATABASE'  
    , @target_object = N'AdventureWorks2012'  
    , @policy_category = N'Table Naming Policies';  
    GO  
    ```  
  
 Para obtener más información, vea [sp_syspolicy_add_policy_category_subscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-add-policy-category-subscription-transact-sql.md).  
  
  