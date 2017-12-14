---
title: Cambiar la disponibilidad de un operador | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssms-agent
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Agent jobs, operators
- canceling operators
- reactivating operators
- removing operators
- deleting operators
- available operators [SQL Server]
- dropping operators
- jobs [SQL Server Agent], operators
- notifications [SQL Server], job status
- disabling operators
- operators (users) [Database Engine], changing availability with Management Studio
ms.assetid: 10d58b92-b67b-47e2-af9c-9f9fd6968bba
caps.latest.revision: "5"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: aef98b74c420cc0f4edc8f4b041db385c6163e70
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/05/2017
---
# <a name="change-an-operator39s-availability"></a>Cambiar la disponibilidad de un operador
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] En este tema se describe cómo cambiar la programación de un operador para recibir notificaciones de alerta en [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] o [!INCLUDE[tsql](../../includes/tsql_md.md)].  
  
**En este tema**  
  
-   **Antes de empezar:**  
  
    [Seguridad](#Security)  
  
-   **Para cambiar la disponibilidad de un operador, utilizando:**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
    [Transact-SQL](#TsqlProcedure)  
  
## <a name="BeforeYouBegin"></a>Antes de comenzar  
  
### <a name="Security"></a>Seguridad  
  
#### <a name="Permissions"></a>Permissions  
Solo los miembros del rol fijo de servidor **sysadmin** pueden editar operadores.  
  
## <a name="SSMSProcedure"></a>Usar SQL Server Management Studio  
  
#### <a name="to-change-an-operators-availability"></a>Para cambiar la disponibilidad de un operador  
  
1.  En el **Explorador de objetos**, haga clic en el signo más para expandir el servidor que contiene el operador que desea habilitar o deshabilitar.  
  
2.  Haga clic en el signo más para expandir **Agente SQL Server**.  
  
3.  Haga clic en el signo más para expandir la carpeta **Operadores** .  
  
4.  Haga clic con el botón derecho en el operador que desea habilitar o deshabilitar y seleccione **Propiedades**; luego, haga clic en la pestaña **General** .  
  
5.  En el cuadro de diálogo *nombre_operador***Propiedades** , active o desactive la casilla **Habilitado** .  
  
6.  Haga clic en **Aceptar**.  
  
## <a name="TsqlProcedure"></a>Usar Transact-SQL  
  
#### <a name="to-change-an-operators-availability"></a>Para cambiar la disponibilidad de un operador  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    -- disables the 'François Ajenstat' operator  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_update_operator   
        @name = N'François Ajenstat',  
        @enabled = 0;  
    GO  
    ```  
  
Para más información, consulte [sp_update_operator (Transact-SQL)](http://msdn.microsoft.com/en-us/231750a6-4828-4d03-afe6-b91d38c42ed3).  
  
