---
title: Registro de aplicación Windows | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- Windows application logs [Reporting Services]
- logs [Reporting Services], Windows application logs
- application logs [Reporting Services]
ms.assetid: 742fd00e-aa6c-4c8a-b58f-c03c489b1699
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 39a36a2c9c5a43c16d3ca54be9e32f81225eace4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47708463"
---
# <a name="windows-application-log"></a>Registro de aplicación Windows
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Escribe mensajes de evento en el registro de aplicación de Windows. Puede utilizar la información de los mensajes escrita en el registro de aplicación para obtener información sobre los eventos generados por las aplicaciones del servidor de informes que se ejecutan en el sistema local.  
  
## <a name="viewing-report-server-events"></a>Ver eventos del servidor de informes  
 Puede utilizar el Visor de eventos para ver el archivo de registro y filtrar los mensajes que contiene. Para obtener más información sobre los mensajes de eventos, vea [Referencia de errores y eventos &#40;Reporting Services&#41;](../../reporting-services/troubleshooting/errors-and-events-reference-reporting-services.md). Para obtener más información sobre el registro de aplicación Windows o el Visor de eventos, consulte la documentación del producto de Windows.  
  
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
  
## <a name="see-also"></a>Ver también  
 [Archivos de registro y orígenes de Reporting Services](../../reporting-services/report-server/reporting-services-log-files-and-sources.md)   
 [Referencia de errores y eventos &#40;Reporting Services&#41;](../../reporting-services/troubleshooting/errors-and-events-reference-reporting-services.md)  
  
  
