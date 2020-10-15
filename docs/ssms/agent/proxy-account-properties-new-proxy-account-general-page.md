---
description: Propiedades de cuenta de proxy - Nueva cuenta de proxy (página General)
title: Propiedades de cuenta de proxy - Nueva cuenta de proxy (página General)
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.proxy.general.f1
ms.assetid: 5cd81265-bf59-413b-8397-150ddc70d0c7
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: a70ba36150771ef90f3cfc9461c018c212da4c73
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/14/2020
ms.locfileid: "92037310"
---
# <a name="proxy-account-properties---new-proxy-account-general-page"></a>Propiedades de cuenta de proxy - Nueva cuenta de proxy (página General)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> En [Azure SQL Managed Instance](/azure/sql-database/sql-database-managed-instance), actualmente son compatibles la mayoría de las características del Agente SQL Server. Consulte [Diferencias entre T-SQL de Azure SQL Managed Instance y SQL Server](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para más información.

Use esta página para ver y cambiar las propiedades de una cuenta de proxy del Agente [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="options"></a>Opciones  
**Nombre del proxy**  
Escriba el nombre del proxy.  
  
**Nombre de credencial**  
Escriba el nombre de la credencial para el proxy.  
  
> [!NOTE]  
> El nombre de la credencial proporcionada debe ser el nombre de una credencial existente. Para obtener más información acerca de la creación de credenciales, vea [Procedimientos para: crear un proxy](../../relational-databases/security/authentication-access/create-a-credential.md)  
  
**...**  
Inicia el cuadro de diálogo **Seleccionar credencial** .  
  
**Descripción**  
Escriba la descripción del proxy.  
  
**Active los siguientes subsistemas:**  
Seleccione los subsistemas a los que tiene acceso la cuenta de proxy.  
  
**Volver a asignar pasos de trabajo a**  
Seleccione el proxy al que se reasignan los pasos de trabajo. Esta lista se habilita cuando se revoca el acceso a un subsistema al que el proxy tenía acceso anteriormente.  
  
## <a name="see-also"></a>Consulte también  
[Create a SQL Server Agent Proxy](../../ssms/agent/create-a-sql-server-agent-proxy.md)  
