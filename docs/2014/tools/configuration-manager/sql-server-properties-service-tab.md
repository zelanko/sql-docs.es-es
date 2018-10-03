---
title: Propiedades de SQL Server (pestaña Servicio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- configmgr-client
ms.topic: conceptual
ms.assetid: e4ae0c6b-6fd8-4325-b54e-1758fc659958
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d69ded06359dfc7f5f7c71864d3be6b64de6f7af
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48227330"
---
# <a name="sql-server-properties-service-tab"></a>Propiedades de SQL Server (pestaña Servicio)
  Utilice la pestaña **Servicio**del cuadro de diálogo **Propiedades de MSSQLSERVER** para ver o especificar las siguientes opciones.  
  
## <a name="options"></a>Opciones  
 **Ruta de acceso binaria**  
 Muestra la ubicación de los archivos de programa utilizados por el servicio.  
  
 **Control de error**  
 1 indica `SERVICE_ERROR_NORMAL`. Si el servicio no se inicia al iniciar el equipo, el programa de inicio registra el error y muestra un cuadro de mensaje emergente pero continúa con la operación de inicio. Este valor no puede modificarse.  
  
 **Código de salida**  
 Si se produce un error, el número de error aparece en este cuadro. Utilice este número para solucionar errores buscando el número en [!INCLUDE[msCoName](../../includes/msconame-md.md)] Knowledge Base o informe del mismo al personal de soporte técnico.  
  
 **Host Name**  
 Muestra el nombre del equipo o clúster que ejecuta el servicio [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Nombre**  
 Indica el nombre para mostrar del servicio.  
  
 **Id. del proceso**  
 Muestra el identificador de proceso de Windows.  
  
 **Tipo de servicio**  
 Muestra el tipo de servicio proporcionado a los procesos de llamada. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instala varios servicios.  
  
 **Modo de inicio**  
 Para este servicio se pueden configurar las siguientes opciones:  
  
-   Manual: el servicio no se inicia automáticamente al iniciar el equipo. Debe iniciarlo mediante el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] u otra herramienta.  
  
-   Automático: el servicio intenta iniciarse cuando se inicia el equipo.  
  
-   Deshabilitado: el servicio no se puede iniciar.  
  
 **State**  
 Indica si el servicio está en ejecución, detenido o deshabilitado. "**…**" indica que hay un cambio de estado pendiente.  
  
  
