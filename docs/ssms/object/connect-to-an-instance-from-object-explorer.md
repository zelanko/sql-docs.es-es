---
title: Conexión a SQL Server o Azure SQL Database | Microsoft Docs
ms.custom: ''
ms.date: 01/28/2019
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: 9803a8a0-a8f1-4b65-87b8-989b06850194
author: markingmyname
ms.author: maghan
manager: jroth
ms.openlocfilehash: 2ce44830eedc410388d44558371dc42f1ee52825
ms.sourcegitcommit: 5d839dc63a5abb65508dc498d0a95027d530afb6
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/09/2019
ms.locfileid: "67690031"
---
# <a name="connect-to-a-sql-server-or-azure-sql-database"></a>Conexión a SQL Server o Azure SQL Database

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Para trabajar con servidores y bases de datos, primero debe conectarse al servidor. Puede conectarse a varios servidores al mismo tiempo.

[SQL Server Management Studio (SSMS)](../download-sql-server-management-studio-ssms.md) admite varios tipos de conexiones. En este artículo se proporcionan detalles para conectarse a SQL Server y Azure SQL Database (mediante la conexión a un grupo elástico o una base de datos única de Azure SQL). Para obtener información sobre las otras opciones de conexión, consulte los [vínculos](#see-also) en la parte inferior de esta página.
  
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

## <a name="next-steps"></a>Next Steps

[Diseño, creación y actualización de tablas](../visual-db-tools/design-tables-visual-database-tools.md)

## <a name="see-also"></a>Consulte también

[SQL Server Management Studio (SSMS)](../sql-server-management-studio-ssms.md)  
[Descarga de SQL Server Management Studio (SSMS)](../download-sql-server-management-studio-ssms.md)

[Analysis Services](https://docs.microsoft.com/sql/analysis-services/instances/connect-to-analysis-services)  
[Integration Services](https://docs.microsoft.com/sql/integration-services/sql-server-integration-services)  
[Reporting Services](https://docs.microsoft.com/sql/reporting-services/tools/connect-to-a-report-server-in-management-studio)  
[Azure Storage](../f1-help/connect-to-microsoft-azure-storage.md)  
