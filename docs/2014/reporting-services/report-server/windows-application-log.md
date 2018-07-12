---
title: Registro de aplicación Windows | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Windows application logs [Reporting Services]
- logs [Reporting Services], Windows application logs
- application logs [Reporting Services]
ms.assetid: 742fd00e-aa6c-4c8a-b58f-c03c489b1699
caps.latest.revision: 31
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 5cc0848226b80c2c77345ed737f8acff68eba5bc
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37150066"
---
# <a name="windows-application-log"></a>Registro de aplicación Windows
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Escribe mensajes de evento en el registro de aplicación de Windows. Puede utilizar la información de los mensajes escrita en el registro de aplicación para obtener información sobre los eventos generados por las aplicaciones del servidor de informes que se ejecutan en el sistema local.  
  
## <a name="viewing-report-server-events"></a>Ver eventos del servidor de informes  
 Puede utilizar el Visor de eventos para ver el archivo de registro y filtrar los mensajes que contiene. Para obtener más información acerca de los mensajes de eventos, consulte [referencia de errores y eventos &#40;Reporting Services&#41;](../troubleshooting/errors-and-events-reference-reporting-services.md). Para obtener más información sobre el registro de aplicación Windows o el Visor de eventos, consulte la documentación del producto de Windows.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] proporciona tres orígenes de eventos:  
  
-   Servidor de informes (servicio Servidor de informes de Windows)  
  
-   Administrador de informes  
  
-   Procesador de entrega y programación  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no proporciona un método para desactivar el registro de eventos de aplicación para un servidor de informes ni para controlar qué eventos se registran. El esquema que describe el registro de eventos del servidor de informes es fijo. No puede extenderlo para que admita eventos personalizados.  
  
 En la tabla siguiente se describen los tipos de eventos que el servidor de informes incluye en el registro de eventos de aplicación.  
  
|Tipo de evento|Descripción|  
|----------------|-----------------|  
|Información|Evento que describe una operación correcta (por ejemplo, cuándo se inicia el servicio del servidor de informes).|  
|Advertencia|Evento que indica un problema potencial (por ejemplo, poco espacio en disco).|  
|Error|Evento que describe un problema considerable (por ejemplo, no se inició el servicio).|  
|Auditoría de aciertos|Evento de seguridad que describe un inicio de sesión correcto.|  
|Auditoría de errores|Evento que se registra cuando se produce un error al intentar iniciar una sesión.|  
  
## <a name="see-also"></a>Vea también  
 [Archivos de registro y orígenes de Reporting Services](../report-server/reporting-services-log-files-and-sources.md)   
 [Referencia de errores y eventos &#40;Reporting Services&#41;](../troubleshooting/errors-and-events-reference-reporting-services.md)  
  
  
