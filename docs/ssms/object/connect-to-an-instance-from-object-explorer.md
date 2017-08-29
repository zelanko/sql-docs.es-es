---
title: "Conexión a SQL Server o Azure SQL Database | Microsoft Docs"
ms.custom: 
ms.date: 08/25/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9803a8a0-a8f1-4b65-87b8-989b06850194
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 21f0cfd102a6fcc44dfc9151750f1b3c936aa053
ms.openlocfilehash: 2d5048825b3c71ecaec5da0f6ae75277994d1697
ms.contentlocale: es-es
ms.lasthandoff: 08/28/2017

---
# <a name="connect-to-a-sql-server-or-azure-sql-database"></a>Conexión a SQL Server o Azure SQL Database

Para trabajar con servidores y bases de datos, primero debe conectarse al servidor. Puede conectarse a varios servidores al mismo tiempo.

[SQL Server Management Studio (SSMS)](../download-sql-server-management-studio-ssms.md) admite varios tipos de conexiones. En este artículo se proporcionan detalles para conectarse a SQL Server y Azure SQL Database (mediante la conexión a un servidor lógico de SQL Azure). Para obtener información sobre las otras opciones de conexión, consulte los [vínculos](#see-also) en la parte inferior de esta página.
  
## <a name="connecting-to-a-server"></a>Conectar a un servidor  

1. En **Explorador de objetos**, haga clic en **Conectar > Motor de base de datos...** .

   ![connect](../media/connect-to-server/connect-db-engine.png)

1. Rellene el formulario **Conectar al servidor** y haga clic en **Conectar**:

   ![Conexión al servidor](../media/connect-to-server/connect.png)

1. Si se está conectando a un servidor SQL de Azure, puede que se le pida que inicie sesión para crear una regla de firewall. Haga clic en **Iniciar sesión...** . Si no es así, vaya directamente al paso 6.

   ![firewall](../media/connect-to-server/firewall-rule-sign-in.png)

1. Después de iniciar sesión correctamente, el formulario se rellenará automáticamente con la dirección IP específica. Si su dirección IP cambia con frecuencia, puede que sea más fácil conceder acceso a un intervalo. Seleccione la opción que sea más adecuada para su entorno. 

   ![firewall](../media/connect-to-server/new-firewall-rule.png)

1. Para crear la regla de firewall y conectarse al servidor, haga clic en **Aceptar**.

1. El servidor se mostrará en el **Explorador de objetos** después de conectarse correctamente:

   ![Conectado](../media/connect-to-server/connected.png)

## <a name="next-steps"></a>Pasos siguientes

[Diseño, creación y actualización de tablas](../visual-db-tools/design-tables-visual-database-tools.md)

## <a name="see-also"></a>Vea también

[SQL Server Management Studio (SSMS)](../sql-server-management-studio-ssms.md)  
[Descarga de SQL Server Management Studio (SSMS)](../download-sql-server-management-studio-ssms.md)

[Analysis Services](https://docs.microsoft.com/sql/analysis-services/instances/connect-to-analysis-services)  
[Integration Services](https://docs.microsoft.com/sql/integration-services/sql-server-integration-services)  
[Reporting Services](https://docs.microsoft.com/sql/reporting-services/tools/connect-to-a-report-server-in-management-studio)  
[Azure Storage](../f1-help/connect-to-microsoft-azure-storage.md)  

