---
title: "Propiedades de Agente SQL Server (página General) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssms-agent
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.ag.agent.general.f1
ms.assetid: b51601e9-5454-43c6-bb5e-24eb2ff043c8
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 92df2d073ff15d955b3e8ee18c83f4b36065c2b2
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/05/2017
---
# <a name="sql-server-agent-properties-general-page"></a>Propiedades de Agente SQL Server (página General)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Use esta página para ver y modificar las propiedades generales del servicio del Agente [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
## <a name="options"></a>Opciones  
**Estado del servicio**  
Muestra el estado actual del servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] .  
  
**Reiniciar SQL Server si se detiene inesperadamente**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] El Agente reinicia [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] si [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] se detiene de forma inesperada.  
  
**Reiniciar el Agente SQL Server automáticamente si se detiene inesperadamente**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] reinicia el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] si el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] se detiene de forma inesperada.  
  
**Nombre de archivo**  
Especifica el nombre de archivo del registro de errores.  
  
**...**  
Permite buscar el archivo del registro de errores.  
  
**Incluir mensajes de seguimiento de ejecución**  
Incluye mensajes de seguimiento de ejecución en el registro de errores. Los mensajes de seguimiento proporcionan información detallada sobre la operación del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] . Por tanto, el archivo de registro requiere más espacio en disco cuando se selecciona esta opción. Solo se debe seleccionar si se intenta solucionar un problema que puede estar relacionado con el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] .  
  
**Escribir archivo OEM**  
Escribe el archivo de registro de errores como un archivo no Unicode. De esta forma, se reduce el espacio en disco que utiliza el archivo de registro. Sin embargo, si se habilita esta opción, puede resultar más difícil leer los mensajes que incluyen datos Unicode.  
  
**Destinatario de NET SEND**  
Escribe el nombre de un operador que recibirá una notificación mediante NET SEND de los mensajes que el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] escribe en el archivo de registro.  
  
## <a name="see-also"></a>Vea también  
[Operadores](../../ssms/agent/operators.md)  
[Registro de errores del Agente SQL Server](../../ssms/agent/sql-server-agent-error-log.md)  
  
