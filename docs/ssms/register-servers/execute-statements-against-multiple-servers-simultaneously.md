---
title: "Ejecutar instrucciones en varios servidores simultáneamente | Microsoft Docs"
ms.custom: 
ms.date: 07/18/2016
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-registration
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- multiserver queries
- executing queries against multiple servers
- queries [SQL Server], multiserver
ms.assetid: 197760f3-0a06-43de-8162-69c27d3fbe56
caps.latest.revision: "21"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 1fa1d9f8250dd3ded83ad41010e4533d6590b898
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="execute-statements-against-multiple-servers-simultaneously"></a>Ejecutar instrucciones en varios servidores simultáneamente
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] En este tema se describe cómo consultar al mismo tiempo varios servidores en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], creando un grupo de servidores locales o bien un Servidor de administración central y uno o varios grupos de servidores, y uno o varios servidores registrados dentro de los grupos, y consultando después el grupo completo. 
  
Los resultados que devuelve la consulta se pueden combinar en un único panel de resultados o en paneles de resultados independientes. El conjunto de resultados puede incluir columnas adicionales para el nombre de servidor y el inicio de sesión que usa la consulta en cada servidor. Los Servidores de administración central y los servidores secundarios se pueden registrar únicamente utilizando la autenticación de Windows. Los servidores de los grupos de servidores locales se pueden registrar con la autenticación de Windows o con la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> **NOTA:** Antes de ejecutar los procedimientos siguientes, cree un Servidor de administración central y un grupo de servidores. Para obtener más información, vea [Crear un servidor de administración central y un grupo de servidores &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/create-a-central-management-server-and-server-group.md).  

  
##  <a name="Permissions"></a> Permissions  
 Dado que las conexiones que mantiene un Servidor de administración central se ejecutan en el contexto del usuario, si se usara la autenticación de Windows, los permisos vigentes en los servidores registrados podrían variar. Por ejemplo, el usuario podría ser miembro del rol fijo de servidor sysadmin en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] A, pero tener permisos limitados en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] B.  
  
 ## <a name="execute-statements-against-multiple-configuration-targets-simultaneously"></a>Ejecutar instrucciones con varios destinos de configuración simultáneamente  

1.  En SQL Server Management Studio, en el menú **Vista** , haga clic en **Servidores registrados**.  
  
2.  Expanda un Servidor de administración central, haga clic con el botón derecho en un grupo de servidores, seleccione **Conectar**y haga clic en **Nueva consulta**.  
  
3.  En el Editor de consultas, escriba y ejecute una instrucción de [!INCLUDE[tsql](../../includes/tsql-md.md)] , como la siguiente:  
  
    ```  
    USE master  
    GO  
    SELECT * FROM sysdatabases;  
    GO  
    ```  
  
     De forma predeterminada, el panel de resultados combinará los resultados de la consulta de todos los servidores del grupo de servidores.  
  
#### <a name="to-change-the-multiserver-results-options"></a>Para cambiar las opciones de los resultados multiservidor  
  
1.  En [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], en el menú **Herramientas** , haga clic en **Opciones**.  
  
2.  Expanda **Resultados de la consulta**, expanda **SQL Server**y, a continuación, haga clic en **Resultados multiservidor**.  
  
3.  En la página **Resultados multiservidor** , especifique la configuración de las opciones que desee y, a continuación, haga clic en **Aceptar**.  
  
## <a name="see-also"></a>Ver también  
 [Administrar varios servidores mediante Servidores de administración central](../../relational-databases/administer-multiple-servers-using-central-management-servers.md)  
  
  
