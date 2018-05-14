---
title: Configuración de las propiedades generales de la administración basada en directivas | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: performance-monitor
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.dmf.PolicyManagement.f1
helpviewer_keywords:
- Policy-Based Management, configure properties
ms.assetid: 6d1e0e37-29ea-408a-a055-384984d884be
caps.latest.revision: 8
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 64b30ee3312aeb3856deb567b3b7d6d4e65131cd
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="configure-the-general-properties-of-policy-based-management"></a>Configurar las propiedades generales de la administración basada en directivas
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  En este tema se describe cómo se configuran las propiedades para la administración basada en directivas de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para configurar la administración basada en directivas se configura con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 Requiere la pertenencia al rol fijo de base de datos PolicyAdministratorRole.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-configure-policy-based-management"></a>Para configurar la administración basada en directivas  
  
1.  En el **Explorador de objetos**, haga clic en el signo más para expandir el servidor en el que quiere configurar las propiedades de administración basada en directivas.  
  
2.  Haga clic en el signo más para expandir la carpeta **Administración** .  
  
3.  Haga clic con el botón derecho en **Administración de directivas** y seleccione **Propiedades**.  
  
     Las siguientes opciones están disponibles en el cuadro de diálogo **Propiedades de Administración de directivas** .  
  
     **Enabled**  
     Especifica si la administración basada en directivas se habilita.  
  
     **HistoryRetentionInDays**  
     Especifica el número de días que se debería conservar el historial de evaluaciones de directivas. Si este valor es 0 (el valor predeterminado), el historial no se quitará automáticamente.  
  
     **LogOnSuccess**  
     Especifica si la administración basada en directivas registra las evaluaciones de la directiva correctas.  
  
    -   Cuando este valor es false (el predeterminado), solo se registran las evaluaciones de las directivas con errores.  
  
    -   Cuando este valor es true, se registran tanto las evaluaciones de directivas correctas como las que tienen errores.  
  
4.  Cuando termine, haga clic en **Aceptar**.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-configure-policy-based-management"></a>Para configurar la administración basada en directivas  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    -- enables Policy-Based Management   
    USE msdb;  
    GO  
    EXEC dbo.sp_syspolicy_configure   
         @name = N'Enabled',   
         @value = 1;  
    GO  
    ```  
  
 Para obtener más información, vea [sp_syspolicy_configure&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-configure-transact-sql.md).  
  
  
