---
description: Propiedades de Agente SQL Server (página General)
title: Propiedades de Agente SQL Server (página General)
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.agent.general.f1
ms.assetid: b51601e9-5454-43c6-bb5e-24eb2ff043c8
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016
ms.openlocfilehash: 91ee6a7d3401d1cecb79dd0a679fa7f277f57012
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97402481"
---
# <a name="sql-server-agent-properties-general-page"></a>Propiedades de Agente SQL Server (página General)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> En [Azure SQL Managed Instance](/azure/sql-database/sql-database-managed-instance), actualmente son compatibles la mayoría de las características del Agente SQL Server. Consulte [Diferencias entre T-SQL de Azure SQL Managed Instance y SQL Server](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para más información.

Use esta página para ver y modificar las propiedades generales del servicio del Agente [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="options"></a>Opciones  
**Estado de servicio**  
Muestra el estado actual del servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
**Reiniciar SQL Server si se detiene inesperadamente**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] El Agente reinicia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] si [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se detiene de forma inesperada.  
  
**Reiniciar el Agente SQL Server automáticamente si se detiene inesperadamente**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] reinicia el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] si el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se detiene de forma inesperada.  
  
**Nombre de archivo**  
Especifica el nombre de archivo del registro de errores.  
  
**...**  
Permite buscar el archivo del registro de errores.  
  
**Incluir mensajes de seguimiento de ejecución**  
Incluye mensajes de seguimiento de ejecución en el registro de errores. Los mensajes de seguimiento proporcionan información detallada sobre la operación del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Por tanto, el archivo de registro requiere más espacio en disco cuando se selecciona esta opción. Solo se debe seleccionar si se intenta solucionar un problema que puede estar relacionado con el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
**Escribir archivo OEM**  
Escribe el archivo de registro de errores como un archivo no Unicode. De esta forma, se reduce el espacio en disco que utiliza el archivo de registro. Sin embargo, si se habilita esta opción, puede resultar más difícil leer los mensajes que incluyen datos Unicode.  
  
**Destinatario de NET SEND**  
Escribe el nombre de un operador que recibirá una notificación mediante NET SEND de los mensajes que el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] escribe en el archivo de registro.  
  
## <a name="see-also"></a>Consulte también  
[Operadores](../../ssms/agent/operators.md)  
[Registro de errores del Agente SQL Server](../../ssms/agent/sql-server-agent-error-log.md)  
