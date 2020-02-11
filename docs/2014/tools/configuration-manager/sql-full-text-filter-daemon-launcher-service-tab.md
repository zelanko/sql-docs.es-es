---
title: Selector de demonio de filtro de texto completo de SQL (pestaña Servicio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: 6aad7ebe-c4be-4d37-8536-61502f51faa2
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6f5129771e5d487075ad2223317047fbbb3c09fe
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68211160"
---
# <a name="sql-full-text-filter-daemon-launcher-service-tab"></a>Selector del demonio de filtro de texto completo de SQL (pestaña Servicio)
  A partir de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], el Selector de demonio de filtro de texto completo de SQL (selector FDHOST) se usa en el texto completo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Este servicio debe estar ejecutándose si se utiliza la búsqueda de texto completo. Para obtener información sobre los procesos de host de demonio de filtro, vea "Arquitectura de la búsqueda de texto completo" en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Use la pestaña **Servicio**del cuadro de diálogo **Propiedades de Selector de demonio de filtro de texto completo de SQL** para ver o especificar las opciones siguientes.  
  
## <a name="options"></a>Opciones  
 **Ruta de acceso binaria**  
 Muestra la ubicación de los archivos de programa utilizados por el servicio.  
  
 **Control de errores**  
 1 indica `SERVICE_ERROR_NORMAL`. Si el servicio no se inicia al iniciar el equipo, el programa de inicio registra el error y muestra un cuadro de mensaje emergente pero continúa con la operación de inicio. No se puede cambiar este valor.  
  
 **Código de salida**  
 Si se produce un error, el número de error aparece en este cuadro. Utilice este número para solucionar errores buscando el número en [!INCLUDE[msCoName](../../includes/msconame-md.md)] Knowledge Base o informe del mismo al personal de soporte técnico.  
  
 **Nombre de host**  
 Muestra el nombre del equipo o clúster que ejecuta el [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servicio.  
  
 **Nombre**  
 Indica el nombre para mostrar del servicio.  
  
 **Identificador del proceso**  
 Muestra el identificador de proceso de Windows.  
  
 **Tipo de servicio SQL**  
 Muestra el tipo de servicio proporcionado a los procesos de llamada. 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instala varios servicios.  
  
 **Modo de inicio**  
 Para este servicio se pueden configurar las siguientes opciones:  
  
-   Manual: el servicio no se inicia automáticamente al iniciar el equipo. Debe iniciarlo mediante el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] u otra herramienta.  
  
-   Automático: el servicio intenta iniciarse cuando se inicia el equipo.  
  
-   Deshabilitado: el servicio no se puede iniciar.  
  
 **State**  
 Indica si el servicio está en ejecución, detenido o deshabilitado. "**…**" indica que hay un cambio de estado pendiente.  
  
  
