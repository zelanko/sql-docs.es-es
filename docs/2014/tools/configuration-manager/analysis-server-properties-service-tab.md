---
title: Propiedades de Analysis Server (pestaña Servicio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: 8dbe4bc5-6aa9-48ee-857e-0b4ea764b9cb
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4f083aafd2dc8718bb79798d43483c66b3520b0d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62666752"
---
# <a name="analysis-server-properties-service-tab"></a>Propiedades de Analysis Server (pestaña Servicio)
  Este es el servicio [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Este servicio debe estar en ejecución para que [!INCLUDE[ssAS](../../includes/ssas-md.md)] funcione correctamente. Los valores de propiedades en color gris claro no se pueden modificar con esta aplicación.  
  
## <a name="options"></a>Opciones  
 **Ruta de acceso binaria**  
 Muestra la ubicación de los archivos de programa utilizados por el servicio.  
  
 **Control de errores**  
 1 indica `SERVICE_ERROR_NORMAL`. Si el servicio no se inicia al iniciar el equipo, el programa de inicio registra el error y muestra un cuadro de mensaje emergente pero continúa con la operación de inicio. Este valor no puede modificarse.  
  
 **Código de salida**  
 Si se produce un error, el número de error aparece en este cuadro. Utilice este número para solucionar errores buscando el número en [!INCLUDE[msCoName](../../includes/msconame-md.md)] Knowledge Base o informe del mismo al personal de soporte técnico.  
  
 **Host Name**  
 Muestra el nombre del equipo o clúster que ejecuta [!INCLUDE[ssAS](../../includes/ssas-md.md)].  
  
 **Name**  
 Indica el nombre para mostrar del servicio.  
  
 **Id. del proceso**  
 Muestra el número que usa [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows para realizar el seguimiento de los procesos de este programa.  
  
 **Tipo de servicio de SQL**  
 Muestra el tipo de servicio proporcionado a los procesos de llamada. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instala varios servicios.  
  
 **Modo de inicio**  
 Para este servicio se pueden configurar las siguientes opciones:  
  
-   Manual: Este servicio no se inicia automáticamente cuando se inicia el equipo. Debe iniciarlo mediante el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] u otra herramienta.  
  
-   Automático: Este servicio intenta iniciarse cuando se inicia el equipo.  
  
-   Deshabilitado: No se puede iniciar este servicio.  
  
 **Estado**  
 Indica si el servicio está en ejecución, detenido o deshabilitado.  
  
  
