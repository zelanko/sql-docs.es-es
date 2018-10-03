---
title: Establecer la opción de configuración del servidor Aumento de prioridad | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- priority boost option
ms.assetid: 765f1e83-dd52-44fb-b0c8-1078f213607b
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: bad83198d31fb2733e0bcc15c5a6a2d19a2b9189
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48224495"
---
# <a name="configure-the-priority-boost-server-configuration-option"></a>Establecer la opción de configuración del servidor Aumento de prioridad
  En este tema se describe cómo configurar la opción de configuración de **aumento de prioridad** en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Use la opción de **aumento de prioridad** para especificar si [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe ejecutarse con una prioridad de programación de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 2008 o Windows 2008 R2 superior a la de otros procesos del mismo equipo. Si establece esta opción en 1, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se ejecutará con una prioridad base de 13 en el programador de Windows 2008 o Windows Server 2008 R2. El valor predeterminado es 0, que equivale a una prioridad base de 7.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   **Para configurar la opción de aumento de prioridad, use:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Seguimiento:**  [Después de configurar la opción de aumento de prioridad](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   El aumento excesivo de la prioridad puede reducir los recursos para funciones fundamentales de la red y del sistema operativo, lo que causaría problemas al cerrar SQL Server o al usar otras tareas del sistema operativo en el servidor.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 De forma predeterminada, todos los usuarios tienen permisos de ejecución en **sp_configure** sin ningún parámetro o solo con el primero. Para ejecutar **sp_configure** con ambos parámetros y cambiar una opción de configuración, o para ejecutar la instrucción RECONFIGURE, un usuario debe tener el permiso ALTER SETTINGS en el servidor. Los roles fijos de servidor **sysadmin** y **serveradmin** tienen el permiso ALTER SETTINGS de forma implícita.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-configure-the-priority-boost-option"></a>Para configurar la opción de aumento de prioridad  
  
1.  En el Explorador de objetos, haga clic con el botón derecho en un servidor y seleccione **Propiedades**.  
  
2.  Haga clic en el nodo **Procesadores** .  
  
3.  En **Subprocesos**, active la casilla **Aumentar la prioridad de SQL Server** .  
  
4.  Detenga y reinicie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-configure-the-priority-boost-option"></a>Para configurar la opción de aumento de prioridad  
  
1.  Conéctese con el [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. En este ejemplo se muestra cómo usar [sp_configure](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql) para establecer el valor de la opción de `priority boost` en `1`.  
  
```tsql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE ;  
GO  
EXEC sp_configure 'priority boost', 1 ;  
GO  
RECONFIGURE;  
GO  
  
```  
  
 Para obtener más información, vea [Opciones de configuración de servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md).  
  
##  <a name="FollowUp"></a> Seguimiento: Después de configurar la opción de aumento de prioridad  
 El servidor debe reiniciarse para que el valor surta efecto.  
  
## <a name="see-also"></a>Vea también  
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [Opciones de configuración de servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
