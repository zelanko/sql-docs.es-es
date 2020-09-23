---
description: Configurar registros de errores del Agente SQL Server (página General)
title: Configuración de registros de errores (página general)
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.errorlog.configure.f1
ms.assetid: e08de622-6f87-470c-aee0-b2d6cb6cca88
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 4236deb3738c4b22dd9c676c96c320f08214b282
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88497658"
---
# <a name="configure-sql-server-agent-error-logs-general-page"></a>Configurar registros de errores del Agente SQL Server (página General)

[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> En [Azure SQL Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), actualmente son compatibles la mayoría de las características del Agente SQL Server. Consulte [Diferencias entre T-SQL de Azure SQL Managed Instance y SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para más información.

Utilice esta pantalla para ver y actualizar la configuración del registro de errores del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="options"></a>Opciones  
**Archivo de registro de errores**  
Especifique el archivo en el que el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] escribe los registros de errores.  
  
**...**  
Permite buscar el archivo del registro de errores.  
  
**Escribir registro de errores OEM**  
Escribe el archivo de registro de errores como un archivo no Unicode. De esta forma, se reduce el espacio en disco que utiliza el archivo de registro. Sin embargo, si se habilita esta opción, puede resultar más difícil leer los mensajes que incluyen datos Unicode.  
  
**Errores**  
Solo escribe errores y mensajes informativos en el archivo de registro.  
  
**Advertencias**  
Solo escribe advertencias y mensajes informativos en el archivo de registro.  
  
**Información**  
Solo escribe mensajes informativos en el archivo de registro.  
  
## <a name="see-also"></a>Consulte también  
[Registro de errores del Agente SQL Server](../../ssms/agent/sql-server-agent-error-log.md)  
  
