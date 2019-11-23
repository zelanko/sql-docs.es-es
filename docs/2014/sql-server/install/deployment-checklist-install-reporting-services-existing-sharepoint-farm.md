---
title: 'Lista de comprobación de implementación: instalar Reporting Services en una granja de servidores de SharePoint existente | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 436b4c3d-3f2f-464a-be7e-5c051d9ffb8f
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: e7a66be0d4e002643ffe1c72ce8c44aa50f61c0e
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952625"
---
# <a name="deployment-checklist-install-reporting-services-into-an-existing-sharepoint-farm"></a>Lista de comprobación de la implementación: instalar Reporting Services en una granja de servidores de SharePoint existente
  Los servidores de informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint se pueden instalar en una granja de servidores de SharePoint nueva o en una existente. En este tema se describen los posibles escenarios y prácticas recomendadas para instalar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en la granja de servidores de SharePoint existente.  
  
## <a name="prerequisites"></a>Prerequisites  
 Antes de ejecutar el programa de instalación, revise la información siguiente:  
  
|Paso|Vínculo|  
|----------|----------|  
|Crear o identificar las cuentas utilizadas en una implementación de un servidor de informes. Debe tener una cuenta de servicio para el servicio del servidor de informes, así como credenciales para la conexión con la base de datos del servidor de informes||  
|Decidir qué instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hospedará la base de datos del servidor de informes. Puede utilizar una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]local o remota Debería elegir una instancia que se encuentre en un equipo con la capacidad de almacenamiento necesaria para sus informes.||  
|(Opcional) Buscar el nombre de la puerta de enlace o el servidor SMTP que proporciona el servicio de correo electrónico a la organización si se va a usar el correo electrónico del servidor de informes en las suscripciones|[Configurar un servidor de informes para la &#40;entrega de correo electrónico en SSRS Configuration Manager&#41;](../../../2014/sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md)|  
|Nota: Si va a actualizar un equipo desde una versión de CTP anterior [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] y ha realizado cambios personalizados en los archivos de configuración, tendrá que realizar los mismos cambios en los archivos de configuración, después de la actualización a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Los archivos afectados son **Web. config** y **Client. config**.||  
  
## <a name="installation-scenarios"></a>Escenarios de instalación  
 En la siguiente tabla se describen los posibles escenarios cuando va a instalar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en una granja de servidores de SharePoint existente. El modo Local permite que los informes se representen localmente desde la biblioteca de documentos de SharePoint, sin integración con un servidor de informes [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Se requiere el complemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para los productos de SharePoint. No se requiere un servidor de informes [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para obtener más información sobre el modo local, vea informes en modo [local frente a modo conectado en &#40;el visor de informes&#41; Reporting Services en modo de SharePoint](../../../2014/reporting-services/local-vs-connected-mode-report-viewer-reporting-services-sharepoint-mode.md) y [dónde encontrar el complemento Reporting Services para productos de SharePoint](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md).  
  
|Iniciar la configuración|Flujo de trabajo|Terminar la configuración|Comentarios|  
|----------------------------|--------------|--------------------------|--------------|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] en modo local|Instalación|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]en modo conectado.||  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] en modo conectado o [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|Actualización en contexto|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]en modo conectado.||  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] en modo conectado o [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|Migración|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]en modo conectado.||  
  
## <a name="installation-and-in-place-upgrade-checklist"></a>Lista de comprobación de la actualización en contexto e instalación  
 En la siguiente tabla se resumen los pasos, herramientas e información que debería revisar y utilizar para la instalación:  
  
|Paso|Vínculo|  
|----------|----------|  
|**Instalación y configuración inicial**||  
|Instale el complemento de SharePoint en todos los equipos front-end web (WFE).|[Incorporación de un front-end web adicional de Reporting Services a una granja de servidores](../../reporting-services/install-windows/add-an-additional-reporting-services-web-front-end-to-a-farm.md)|  
|Instalar SQL Server [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Reporting Services y el motor de base de datos.|[Instalar el modo de SharePoint de Reporting Services para SharePoint 2010](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)|  
|Crear al menos una aplicación de servicio de Reporting Services y configurar la asociación de las aplicaciones de servicio.|Vea la sección "aplicación de servicio" en [instalar el modo de SharePoint de Reporting Services para sharepoint 2010](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)|  
|**Configuración adicional**||  
|Agregar tipos de contenido SSRS a la biblioteca de documentos.|[Agregar tipos de contenido del servidor de informes &#40;a una biblioteca Reporting Services en el modo integrado de SharePoint&#41;](../../../2014/reporting-services/add-reporting-services-content-types-to-a-sharepoint-library.md)|  
|Aprovisionar el Agente SQL Server|[Aprovisionamiento de subscripciones y alertas para aplicaciones de servicio de SSRS](../../reporting-services/install-windows/provision-subscriptions-and-alerts-for-ssrs-service-applications.md)|  
|Configurar las opciones de correo electrónico para la aplicación de servicio|[Configurar el correo electrónico para una aplicación de servicio de Reporting Services &#40;SharePoint 2010 y SharePoint 2013&#41;](../../reporting-services/install-windows/configure-e-mail-for-a-reporting-services-service-application.md)|  
|Configurar Notificaciones al servicio de token de Windows (c2WTS)|[Notificaciones del servicio &#40;de token&#41; de Windows C2WTS y Reporting Services](../../../2014/sql-server/install/claims-to-windows-token-service-c2wts-and-reporting-services.md)|  
  
## <a name="migration-checklist"></a>Lista de comprobación de la migración  
 La siguiente es una lista de los pasos básicos para realizar la migración de una instalación existente a una nueva instalación.  
  
|Paso|Vínculo|  
|----------|----------|  
|Instalar y configurar el nuevo servidor. Incluye lo siguiente:<br /><br /> Herramienta de preparación de productos de SharePoint<br /><br /> Producto SharePoint 2010<br /><br /> SharePoint 2010 SP1<br /><br /> [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en modo de SharePoint<br /><br /> Complemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para productos de SharePoint 2010|[Instalar el modo de SharePoint de Reporting Services para SharePoint 2010](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)|  
|Crear por lo menos una aplicación de servicio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]||  
|Realizar la copia de seguridad de las bases de datos de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]||  
|Realizar la copia de seguridad de las claves de cifrado de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]||  
|Restaurar la base de datos de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y las claves de cifrado||  
|Asignar todas las aplicaciones web a las nuevas aplicaciones de servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|La nueva instalación **es funcional ahora**|  
|Quitar la integración de direcciones URL en el servidor anterior.|Desde Administración central de SharePoint, en la Página **Configuración de aplicación general** , haga clic en **Integración de Reporting Services**.|  
|Desinstalar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] desde la anterior instalación, si lo desea.||  
  
## <a name="next-steps"></a>Next Steps  
  
## <a name="see-also"></a>Vea también  
 [Instalación &#40;del modo de SharePoint de Reporting Services SharePoint 2010&#41; y SharePoint 2013](../../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md)   
 [Instrucciones para usar las características de SQL Server BI en una granja de servidores de SharePoint 2010](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md)   
 [Combinaciones admitidas de SharePoint y Reporting Services Server y el complemento &#40;SQL Server 2014&#41;](../../reporting-services/install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md)  
  
  
