---
title: Propiedades de Agente SQL Server (página Conexión)
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.agent.connection.f1
ms.assetid: d6a677ff-60ad-47ba-a0cb-df4193b165e0
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: e2edbc16241c3817ca6cd8ba17e3e82ec1b3471f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85755134"
---
# <a name="sql-server-agent-properties-connection-page"></a>Propiedades de Agente SQL Server (página Conexión)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> En [Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), la mayoría de las características de agente SQL Server son compatibles actualmente, aunque no todas. Vea [Diferencias de T-SQL en Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para obtener más información.

Utilice esta página para ver y modificar la configuración de la conexión del servicio Agente [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="options"></a>Opciones  
**Servidor de host local del alias**  
Especifica el alias que debe utilizarse para conectarse a la instancia local de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si no puede utilizar las opciones de conexión predeterminadas del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , defina un alias para la instancia y especifíquelo aquí.  
  
**Utilizar autenticación de Windows**  
Establece la autenticación de [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows como método de autenticación que se utiliza para conectarse a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se conecta como la cuenta con la que se ejecuta el servicio Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
**Utilizar autenticación de SQL Server**  
Establece la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como método de autenticación que se utiliza para conectarse a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!IMPORTANT]  
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se proporciona por motivos de compatibilidad con versiones anteriores. Para mejorar la seguridad, utilice la autenticación de Windows siempre que sea posible.  
  
**Inicio de sesión**  
Especifica el nombre de inicio de sesión que debe utilizarse para conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
**Contraseña**  
Especifica la contraseña que debe utilizarse para conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
