---
title: Visor de archivos de registro | Microsoft Docs
description: Use el Visor del archivo de registro de SQL Server Management Studio para obtener información sobre los errores y eventos capturados en los archivos de registro.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- Log File Viewer
ms.assetid: a4ea7fc8-1cb2-4c98-bc86-8991c5e748b2
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 7425bb2175b9a2e7b813f63e7d78aec7e73ef5ec
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85668125"
---
# <a name="log-file-viewer"></a>Visor de archivos de registro
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  El Visor del archivo de registros de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] se usa para obtener acceso a la información sobre los errores y eventos capturados en los archivos de registro.  
  
## <a name="benefits-of-using-log-file-viewer"></a>Ventajas de usar el visor del archivo de registro  
 Puede ver los archivos de registro de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desde una instancia local o remota de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuando la instancia de destino está sin conexión o no se puede iniciar. Puede tener acceso a los archivos de registro sin conexión de servidores registrados o mediante programación a través de consultas WMI y WQL (Lenguaje de la consulta de WMI). Para obtener más información, vea [Ver sin conexión archivos de registro](../../relational-databases/logs/view-offline-log-files.md). Estos son los tipos de archivos de registro a que se puede tener acceso con el visor del archivo de registro:  
  
-   Recopilación de auditoría  
  
-   Recopilación de datos  
  
-   Correo electrónico de base de datos  
  
-   Historial de trabajos  
  
-   Planes de mantenimiento  
  
-   Planes de mantenimiento remoto  
  
-   SQL Server  
  
-   Agente SQL Server  
  
-   Windows NT (se puede tener acceso a estos eventos de Windows también desde el Visor de eventos).  
  
## <a name="log-file-viewer-tasks"></a>Tareas del visor del archivo de registros  
  
|Descripción de la tarea|Tema|  
|----------------------|-----------|  
|Describe cómo abrir el visor del archivo de registros dependiendo de la información que se desee ver.|[Abrir el Visor de archivos de registro](../../relational-databases/logs/open-log-file-viewer.md)|  
|Describe cómo ver los archivos de registro sin conexión a través de servidores registrados y cómo comprobar los permisos de WMI.|[Ver archivos del registro sin conexión](../../relational-databases/logs/view-offline-log-files.md)|  
|Proporciona la Ayuda F1 del visor del archivo de registro.|[Ayuda F1 del Visor de archivos de registro](../../relational-databases/logs/log-file-viewer-f1-help.md)|  
  
## <a name="see-also"></a>Consulte también  
 [SQL Server Audit &#40;motor de base de datos&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)   
 [Registro de errores del Agente SQL Server](../../ssms/agent/sql-server-agent-error-log.md)  
  
  
