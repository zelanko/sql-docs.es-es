---
description: Conexión a SQL Server o Azure SQL Database
title: Conexión a SQL Server o Azure SQL Database
ms.custom: seo-lt-2019
ms.date: 01/28/2019
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: 9803a8a0-a8f1-4b65-87b8-989b06850194
author: markingmyname
ms.author: maghan
ms.openlocfilehash: bd161a78bb0b5249d0ce6f802760acd2048014f6
ms.sourcegitcommit: 67befbf7435f256e766bbce6c1de57799e1db9ad
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/24/2020
ms.locfileid: "92523984"
---
# <a name="connect-to-a-sql-server-or-azure-sql-database"></a>Conexión a SQL Server o Azure SQL Database

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
Para trabajar con servidores y bases de datos, primero debe conectarse al servidor. Puede conectarse a varios servidores al mismo tiempo.

[SQL Server Management Studio (SSMS)](../download-sql-server-management-studio-ssms.md) admite varios tipos de conexiones. En este artículo se proporcionan detalles para conectarse a SQL Server y Azure SQL Database (mediante la conexión a un grupo elástico o una base de datos única de Azure SQL). Para obtener información sobre las otras opciones de conexión, consulte los [vínculos](#see-also) en la parte inferior de esta página.
  
## <a name="connecting-to-a-server"></a>Conectar a un servidor  

1. En **Explorador de objetos** , haga clic en **Conectar > Motor de base de datos...**.

   ![conectar](../media/connect-to-server/connect-db-engine.png)

1. Rellene el formulario **Conectar al servidor** y haga clic en **Conectar** :

   ![conectar con el servidor](../media/connect-to-server/connect.png)

1. Si se está conectando a un servidor SQL de Azure, puede que se le pida que inicie sesión para crear una regla de firewall. Haga clic en **Iniciar sesión...**. Si no es así, vaya directamente al paso 6.

   ![Captura de pantalla del cuadro de diálogo Nueva regla de firewall con la opción Iniciar sesión seleccionada.](../media/connect-to-server/firewall-rule-sign-in.png)

1. Después de iniciar sesión correctamente, el formulario se rellenará automáticamente con la dirección IP específica. Si su dirección IP cambia con frecuencia, puede que sea más fácil conceder acceso a un intervalo. Seleccione la opción que sea más adecuada para su entorno. 

   ![Captura de pantalla del cuadro de diálogo Nueva regla de firewall con las opciones Agregar la IP de mi cliente y Aceptar seleccionadas.](../media/connect-to-server/new-firewall-rule.png)

1. Para crear la regla de firewall y conectarse al servidor, haga clic en **Aceptar**.

1. El servidor se mostrará en el **Explorador de objetos** después de conectarse correctamente:

   ![connected](../media/connect-to-server/connected.png)

## <a name="next-steps"></a>Pasos siguientes

[Diseño, creación y actualización de tablas](../visual-db-tools/design-tables-visual-database-tools.md)

## <a name="see-also"></a>Consulte también

[SQL Server Management Studio (SSMS)](../sql-server-management-studio-ssms.md)  
[Descarga de SQL Server Management Studio (SSMS)](../download-sql-server-management-studio-ssms.md)

[Analysis Services](/analysis-services/instances/connect-from-client-applications-analysis-services)  
[Servicio de integración](../../integration-services/sql-server-integration-services.md)  
[Reporting Services](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)  
[Almacenamiento de Azure](../f1-help/connect-to-microsoft-azure-storage.md)