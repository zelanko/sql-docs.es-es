---
title: Propiedades de SQL Server Integration Services (pestaña Servicio) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: 37f0acd9-c96f-48fd-9b53-2ca0097af242
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d4cb1b821604d125bc81148a06fb613c8547a449
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68186720"
---
# <a name="sql-server-integration-services-properties-service-tab"></a>Propiedades de SQL Server Integration Services (pestaña Servicio)
  Use la pestaña **Servicio** del cuadro de diálogo Propiedades[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ** de ** para ver o especificar las siguientes opciones.  
  
## <a name="options"></a>Opciones  
 **Ruta de acceso binaria**  
 Muestra la ubicación de los archivos de programa utilizados por el servicio.  
  
 **Control de errores**  
 1 indica `SERVICE_ERROR_NORMAL`. Si el servicio no se inicia al iniciar el equipo, el programa de inicio registra el error y muestra un cuadro de mensaje emergente pero continúa con la operación de inicio. No se puede cambiar este valor.  
  
 **Código de salida**  
 Código de error de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows que define los problemas encontrados al iniciar o detener el servicio. Esta propiedad se establece en **ERROR_SERVICE_SPECIFIC_ERROR** (1066) si el error es exclusivo del servicio representado por esta clase y hay información disponible sobre el error en la propiedad **ServiceSpecificExitCode** . El servicio establece este valor en NO_ERROR (0) cuando se ejecuta, y de nuevo cuando finaliza normalmente.  
  
 **Nombre de host**  
 Muestra el nombre del equipo o clúster que ejecuta el servicio [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 **Nombre**  
 Indica el nombre para mostrar del servicio.  
  
 **Identificador del proceso**  
 Muestra el identificador de proceso de Windows.  
  
 **Tipo de servicio SQL**  
 Muestra el tipo de servicio proporcionado a los procesos de llamada. [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instala varios servicios.  
  
 **Modo de inicio**  
 Para este servicio se pueden configurar las siguientes opciones:  
  
-   Manual: el servicio no se inicia automáticamente al iniciar el equipo. Debe iniciarlo mediante el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] u otra herramienta.  
  
-   Automático: el servicio intenta iniciarse cuando se inicia el equipo.  
  
-   Deshabilitado: el servicio no se puede iniciar.  
  
 **State**  
 Indica si el servicio está en ejecución, detenido o deshabilitado. "**…**" indica que hay un cambio de estado pendiente.  
  
  
