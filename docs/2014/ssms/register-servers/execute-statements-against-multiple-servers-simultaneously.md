---
title: Ejecutar instrucciones con varios servidores simultáneamente (SQL Server Management Studio) | Documentos de Microsoft
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
- multiserver queries
- executing queries against multiple servers
- queries [SQL Server], multiserver
ms.assetid: 197760f3-0a06-43de-8162-69c27d3fbe56
caps.latest.revision: 20
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 91c0819053860f6ea825890fdafedf05b9041d95
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36198583"
---
# <a name="execute-statements-against-multiple-servers-simultaneously-sql-server-management-studio"></a>Ejecutar instrucciones con varios servidores simultáneamente (SQL Server Management Studio)
  En este tema se describe cómo consultar al mismo tiempo varios servidores en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]creando un grupo de servidores locales o un Servidor de administración central y uno o varios grupos de servidores, y uno o varios servidores registrados dentro de los grupos, y consultando a continuación el grupo completo. Los resultados que devuelve la consulta se pueden combinar en un único panel de resultados o en paneles de resultados independientes. El conjunto de resultados puede incluir columnas adicionales para el nombre de servidor y el inicio de sesión que usa la consulta en cada servidor. Los Servidores de administración central y los servidores secundarios se pueden registrar únicamente utilizando la autenticación de Windows. Los servidores de los grupos de servidores locales se pueden registrar con la autenticación de Windows o con la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  Antes de ejecutar los procedimientos siguientes, cree un Servidor de administración central y grupos de servidores. Para obtener más información, vea [Crear un servidor de administración central y un grupo de servidores &#40;SQL Server Management Studio&#41;](create-a-central-management-server-and-server-group.md).  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para ejecutar instrucciones en varios servidores, mediante:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 Dado que las conexiones que mantiene un Servidor de administración central se ejecutan en el contexto del usuario, si se usara la autenticación de Windows, los permisos vigentes en los servidores registrados podrían variar. Por ejemplo, el usuario podría ser miembro del rol fijo de servidor sysadmin en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] A, pero tener permisos limitados en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] B.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-execute-statements-against-multiple-configuration-targets-simultaneously"></a>Para ejecutar instrucciones con varios destinos de configuración simultáneamente  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], en el menú **Ver** , haga clic en **Servidores registrados**.  
  
2.  Expanda un Servidor de administración central, haga clic con el botón secundario en un grupo de servidores, seleccione **Conectar**y, a continuación, haga clic en **Nueva consulta**.  
  
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
  
## <a name="see-also"></a>Vea también  
 [Administrar varios servidores mediante Servidores de administración central](../../relational-databases/administer-multiple-servers-using-central-management-servers.md)  
  
  