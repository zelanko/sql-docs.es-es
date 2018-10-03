---
title: Abrir proyectos de Integration Services en Data Quality Client | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- data-quality-services
ms.topic: conceptual
ms.assetid: a8bad2f1-8fb0-4d14-a978-11a5720e62d6
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 83f0fc91260bc3e524c323a6d22d2e217df9267d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48105415"
---
# <a name="open-integration-services-projects-in-data-quality-client"></a>Abrir proyectos de Integration Services en Data Quality Client
  El [!INCLUDE[ssDQSCleansingLong](../includes/ssdqscleansinglong-md.md)] le permite ejecutar un proyecto de limpieza en modo por lotes. Sin embargo, en ocasiones es posible que desee revisar los resultados de la limpieza en un paquete de Integration Services de forma parecida a como se hace en la pestaña **Administrar y ver resultados** de una actividad de limpieza en un proyecto de calidad de datos de DQS. DQS le permite abrir proyectos de Integration Services en la pantalla [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] Abrir proyecto **de** como si fuera cualquier otro proyecto de calidad de datos, así como disfrutar de una experiencia interactiva de limpieza de los resultados de limpieza en ellos.  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="LimitationsRestrictions"></a> Limitaciones y restricciones  
  
-   En la pantalla **Abrir proyecto** de [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]solo están disponibles los proyectos de Integration Services que están completos. Los proyectos con errores o en ejecución no están disponibles en la pantalla **Abrir proyecto** .  
  
-   Los proyectos de Integration Services se abren en la fase de limpieza interactiva (pestaña**Administrar y ver resultados** ) en [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]. No puede desplazarse a las pestañas **Limpieza** o **Asignación** . Solo puede ir a la pestaña **Exportar** haciendo clic en **Siguiente**.  
  
-   No es posible eliminar un proyecto de Integration Services bloqueado desde [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]. Para poder eliminarlo, primero debe desbloquearlo.  
  
###  <a name="Prerequisites"></a> Requisitos previos  
 Para ver y abrir en [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]un proyecto de Integration Services que contiene un paquete con un componente de limpieza de DQS, primero debe haber completado correctamente su ejecución.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 Debe disponer del rol dqs_kb_editor o dqs_kb_operator en la base de datos DQS_MAIN para abrir un proyecto de Integration Services.  
  
 ![Icono de flecha usado con el vínculo volver al principio](../2014-toc/media/uparrow16x16.gif "icono de flecha usado con el vínculo volver al principio") [en este tema](#Intro)  
  
##  <a name="Open"></a> Abrir un proyecto de Integration Services  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Ejecute la aplicación Data Quality Client](../../2014/data-quality-services/run-the-data-quality-client-application.md).  
  
2.  En la página de inicio de [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , haga clic en **Abrir proyecto de calidad de datos**. Aparece la pantalla **Abrir proyecto** .  
  
3.  En la pantalla **Abrir proyecto** , puede identificar un proyecto de Integration Services de una de las formas siguientes:  
  
    1.  **Nombre del proyecto**: Los proyectos de Integration Services se muestran con la terminología de nomenclatura siguiente: "Package.DQS Cleansing_*\<FECHA>**\<HORA>*_{GUID}". Cada vez que ejecuta correctamente el mismo paquete en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], aparece un nuevo proyecto en la pantalla **Abrir proyecto** .  
  
    2.  **Tipo de proyecto**: los proyectos de Integration Services tienen **SSIS** como tipo de proyecto en la pantalla **Abrir proyecto** .  
  
     Seleccione un proyecto y haga clic en **Siguiente**.  
  
4.  El proyecto de Integration Services se abre en la fase de limpieza interactiva (pestaña**Administrar y ver resultados** ). Si lo desea, puede realizar una limpieza interactiva en los datos del proyecto de Integration Services. Para obtener información detallada sobre la pestaña **Administrar y ver resultados**, vea [Fase de limpieza interactiva](../../2014/data-quality-services/cleanse-data-using-dqs-internal-knowledge.md#Interactive) en [Limpiar datos mediante el conocimiento de DQS &#40;interno&#41;](../../2014/data-quality-services/cleanse-data-using-dqs-internal-knowledge.md).  
  
5.  Haga clic en **Siguiente** para ir a la pestaña **Exportar** , desde donde podrá exportar los datos procesados a una nueva tabla de la base de datos de SQL Server, un archivo .csv o un archivo de Excel. Para obtener información detallada sobre la pestaña **Exportar**, vea [Fase de exportación](../../2014/data-quality-services/cleanse-data-using-dqs-internal-knowledge.md#Export) en [Limpiar datos mediante el conocimiento de DQS &#40;interno&#41;](../../2014/data-quality-services/cleanse-data-using-dqs-internal-knowledge.md).  
  
6.  Una vez exportados los datos, haga clic en **Finalizar** para cerrar el proyecto de Integration Services.  
  
 ![Icono de flecha usado con el vínculo volver al principio](../2014-toc/media/uparrow16x16.gif "icono de flecha usado con el vínculo volver al principio") [en este tema](#Intro)  
  
## <a name="see-also"></a>Vea también  
 [Transformación Limpieza de DQS](../integration-services/data-flow/transformations/dqs-cleansing-transformation.md)   
 [Servicios de integración &#40;SSIS&#41; proyectos](../integration-services/integration-services-ssis-projects-and-solutions.md)  
  
  
