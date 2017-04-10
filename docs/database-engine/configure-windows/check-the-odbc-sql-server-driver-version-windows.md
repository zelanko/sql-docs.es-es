---
title: "Comprobar la versi&#243;n del controlador ODBC de SQL Server (Windows) | Microsoft Docs"
ms.custom: ""
ms.date: "11/07/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "número de versión del controlador [ODBC]"
  - "Controladores ODBC, número de versión"
ms.assetid: 43451080-a562-4231-b1d4-1ba35ca0ea79
caps.latest.revision: 23
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 23
---
# Comprobar la versi&#243;n del controlador ODBC de SQL Server (Windows)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Su equipo puede contener varios controladores ODBC, de [!INCLUDE[msCoName](../../includes/msconame-md.md)] y de otras empresas. En este tema se describe cómo usar el **Administrador de orígenes de datos ODBC** de Windows para comprobar la versión de los controladores ODBC instalados.  
  
##  <a name="SSMSProcedure"></a>  
  
#### <a name="to-check-the-odbc-sql-server-driver-version-32bit-odbc"></a>Para comprobar la versión del controlador ODBC de SQL Server (ODBC de 32 bits)  
  
-   En el **Administrador de origen de datos ODBC**, haga clic en la pestaña **Controladores** .  
  
     La información de la entrada de Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se muestra en la columna **Versión** .  


> [!NOTE]  
>  En el caso de conexiones a Azure Active Directory Authentication para SQL Database, instale el controlador más reciente, como [ODBC Driver 13.1 for SQL Server](https://www.microsoft.com/download/details.aspx?id=53339).   

  
## <a name="see-also"></a>Vea también  
 [Abrir el Administrador de orígenes de datos ODBC](../../database-engine/configure-windows/open-the-odbc-data-source-administrator.md)  
  
  