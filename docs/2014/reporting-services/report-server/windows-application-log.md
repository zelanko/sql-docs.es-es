---
title: Registro de aplicación Windows | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Windows application logs [Reporting Services]
- logs [Reporting Services], Windows application logs
- application logs [Reporting Services]
ms.assetid: 742fd00e-aa6c-4c8a-b58f-c03c489b1699
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 747a811d1d355bd182b18f4c29f2d1bf9354fa55
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66103026"
---
# <a name="windows-application-log"></a>Registro de aplicación Windows
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Escribe mensajes de evento en el registro de aplicación de Windows. Puede utilizar la información de los mensajes escrita en el registro de aplicación para obtener información sobre los eventos generados por las aplicaciones del servidor de informes que se ejecutan en el sistema local.  
  
## <a name="viewing-report-server-events"></a>Ver eventos del servidor de informes  
 Puede utilizar el Visor de eventos para ver el archivo de registro y filtrar los mensajes que contiene. Para obtener más información sobre los mensajes de eventos, vea [Referencia de errores y eventos &#40;Reporting Services&#41;](../troubleshooting/errors-and-events-reference-reporting-services.md). Para obtener más información sobre el registro de aplicación Windows o el Visor de eventos, consulte la documentación del producto de Windows.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] proporciona tres orígenes de eventos:  
  
-   Servidor de informes (servicio Servidor de informes de Windows)  
  
-   Administrador de informes  
  
-   Procesador de entrega y programación  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no proporciona un método para desactivar el registro de eventos de aplicación para un servidor de informes ni para controlar qué eventos se registran. El esquema que describe el registro de eventos del servidor de informes es fijo. No puede extenderlo para que admita eventos personalizados.  
  
 En la tabla siguiente se describen los tipos de eventos que el servidor de informes incluye en el registro de eventos de aplicación.  
  
|Tipo de evento|Descripción|  
|----------------|-----------------|  
|Information|Evento que describe una operación correcta (por ejemplo, cuándo se inicia el servicio del servidor de informes).|  
|Advertencia|Evento que indica un problema potencial (por ejemplo, poco espacio en disco).|  
|Error|Evento que describe un problema considerable (por ejemplo, no se inició el servicio).|  
|Auditoría de aciertos|Evento de seguridad que describe un inicio de sesión correcto.|  
|Auditoría de errores|Evento que se registra cuando se produce un error al intentar iniciar una sesión.|  
  
## <a name="see-also"></a>Consulte también  
 [Archivos de registro y orígenes de Reporting Services](../report-server/reporting-services-log-files-and-sources.md)   
 [Referencia de errores y eventos &#40;Reporting Services&#41;](../troubleshooting/errors-and-events-reference-reporting-services.md)  
  
  
