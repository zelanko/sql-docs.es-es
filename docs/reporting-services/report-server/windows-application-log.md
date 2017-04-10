---
title: "Registro de aplicaci&#243;n Windows | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "registros de aplicación Windows [Reporting Services]"
  - "registros [Reporting Services], registros de aplicación Windows"
  - "registros de aplicación [Reporting Services]"
ms.assetid: 742fd00e-aa6c-4c8a-b58f-c03c489b1699
caps.latest.revision: 32
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 32
---
# Registro de aplicaci&#243;n Windows
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Escribe mensajes de evento en el registro de aplicación de Windows. Puede utilizar la información de los mensajes escrita en el registro de aplicación para obtener información sobre los eventos generados por las aplicaciones del servidor de informes que se ejecutan en el sistema local.  
  
## Ver eventos del servidor de informes  
 Puede utilizar el Visor de eventos para ver el archivo de registro y filtrar los mensajes que contiene. Para obtener más información sobre los mensajes de eventos, vea [Referencia de errores y eventos &#40;Reporting Services&#41;](../../reporting-services/troubleshooting/errors-and-events-reference-reporting-services.md). Para obtener más información sobre el registro de aplicación Windows o el Visor de eventos, consulte la documentación del producto de Windows.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] proporciona tres orígenes de eventos:  
  
-   Servidor de informes (servicio Servidor de informes de Windows)  
  
-   Administrador de informes  
  
-   Procesador de entrega y programación  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no proporciona un método para desactivar el registro de eventos de aplicación para un servidor de informes ni para controlar qué eventos se registran. El esquema que describe el registro de eventos del servidor de informes es fijo. No puede extenderlo para que admita eventos personalizados.  
  
 En la tabla siguiente se describen los tipos de eventos que el servidor de informes incluye en el registro de eventos de aplicación.  
  
|Tipo de evento|Description|  
|----------------|-----------------|  
|Información|Evento que describe una operación correcta (por ejemplo, cuándo se inicia el servicio del servidor de informes).|  
|Advertencia|Evento que indica un problema potencial (por ejemplo, poco espacio en disco).|  
|Error|Evento que describe un problema considerable (por ejemplo, no se inició el servicio).|  
|Auditoría de aciertos|Evento de seguridad que describe un inicio de sesión correcto.|  
|Auditoría de errores|Evento que se registra cuando se produce un error al intentar iniciar una sesión.|  
  
## Vea también  
 [Archivos de registro y orígenes de Reporting Services](../../reporting-services/report-server/reporting-services-log-files-and-sources.md)   
 [Referencia de errores y eventos &#40;Reporting Services&#41;](../../reporting-services/troubleshooting/errors-and-events-reference-reporting-services.md)  
  
  