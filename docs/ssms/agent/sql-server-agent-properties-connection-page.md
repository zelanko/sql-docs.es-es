---
description: Propiedades de Agente SQL Server (página Conexión)
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
ms.openlocfilehash: f2613cac32463e0711f4de529e5cabb2d2a9885f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88480273"
---
# <a name="sql-server-agent-properties-connection-page"></a>Propiedades de Agente SQL Server (página Conexión)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> En [Azure SQL Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), actualmente son compatibles la mayoría de las características del Agente SQL Server. Consulte [Diferencias entre T-SQL de Azure SQL Managed Instance y SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para más información.

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
  
