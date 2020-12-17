---
description: Force a Target Server to Poll the Master Server
title: Force a Target Server to Poll the Master Server
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- forcing master server polling
- polling master servers [SQL Server]
- master servers [SQL Server], polling
- target servers [SQL Server], polling the master server
ms.assetid: f1189a47-5ac3-45e2-9c5f-847810672279
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016
ms.openlocfilehash: 4aaac1b02996efdf950e4a0fecac054b25a9055c
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97474466"
---
# <a name="force-a-target-server-to-poll-the-master-server"></a>Force a Target Server to Poll the Master Server
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> En [Azure SQL Managed Instance](/azure/sql-database/sql-database-managed-instance), actualmente son compatibles la mayoría de las características del Agente SQL Server. Consulte [Diferencias entre T-SQL de Azure SQL Managed Instance y SQL Server](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para más información.

En este tema se describe cómo forzar que un servidor de destino sondee el servidor maestro. El servidor de destino debe ser un servidor registrado en el servidor maestro.  
  
Un trabajo es una serie especificada de acciones que realiza el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Un trabajo multiservidor es un trabajo que ejecuta un servidor maestro en uno o más servidores de destino. Cada servidor de destino puede ejecutar una instancia del mismo trabajo al mismo tiempo. Cada servidor de destino sondea periódicamente al servidor maestro, descarga una copia de cualquier nuevo trabajo asignado al servidor de destino y, a continuación, se desconecta. El servidor de destino ejecuta el trabajo de manera local y, a continuación, se vuelve a conectar al servidor maestro para cargar el estado del resultado del trabajo.  
  
> [!NOTE]  
> Si no es posible el acceso al servidor maestro cuando el servidor de destino intenta cargar el estado del trabajo, dicho estado de trabajo se coloca en la cola hasta que se pueda obtener acceso al servidor principal.  
  
-   **Antes de empezar:**  [Limitaciones y restricciones](#Restrictions), [Seguridad](#Security)  
  
-   **Acción de forzar que un servidor de destino sondee el servidor maestro utilizando lo siguiente:** [SQL Server Management Studio](#SSMS)  
  
## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>Antes de empezar  
  
### <a name="limitations-and-restrictions"></a><a name="Restrictions"></a>Limitaciones y restricciones  
El servidor de destino debe ser un servidor registrado en el servidor maestro. Debe ejecutar las instrucciones proporcionadas en este tema desde el servidor maestro.  
  
### <a name="security"></a><a name="Security"></a>Seguridad  
Para obtener información detallada, vea [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md) y [Choose the Right SQL Server Agent Service Account for Multiserver Environments](../../ssms/agent/choose-the-right-sql-server-agent-service-account-for-multiserver-environments.md).  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMS"></a>Usar SQL Server Management Studio  
**Para forzar que un servidor de destino sondee el servidor maestro**  
  
1.  En el **Explorador de objetos**, expanda el servidor maestro.  
  
2.  Haga clic con el botón derecho en **Agente SQL Server**, seleccione **Administración multiservidor** y, luego, haga clic en **Administrar servidores de destino**.  
  
3.  Haga clic en un servidor de destino y, a continuación, haga clic en **Forzar sondeo**.  
