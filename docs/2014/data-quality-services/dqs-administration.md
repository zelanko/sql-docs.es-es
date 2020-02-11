---
title: Administración de DQS | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
helpviewer_keywords:
- dqs administration
- administration
- dqs,adminstration
ms.assetid: 9940ef5d-f6f6-4dec-9414-1077a4d7f12b
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 7f4ddc16bdfcc7e0d3acdfabe83e81f3d06c0b93
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "70154438"
---
# <a name="dqs-administration"></a>dqs, administración
  
  [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) permite administrar diversas actividades de DQS realizadas en [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)], configurar las propiedades del servidor relacionadas con las actividades de DQS, configurar los valores de Reference Data Service y configurar los valores del registro de DQS. Todo esto se realizan a través de la característica **Administración** en [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]. En función del acceso de seguridad (rol) en DQS, se le concede o deniega el acceso a diversas funcionalidades de esta área.  
  
 Además de estas actividades de administración, en este tema, también se ofrece información sobre la actividad de administración, copias de seguridad y restauración de bases de datos de DQS, que no se realizan mediante [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)].  
  
 La característica de administración de [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] tiene las siguientes ventajas:  
  
-   Permite a los administradores de datos supervisar diversas actividades de DQS en un [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] de [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)].  
  
-   Permite a los administradores de DQS supervisar las actividades de DQS en un [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] de [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]y *finalizar* una actividad en ejecución o *detener* un proceso en ejecución dentro de una actividad, si así se requiere.  
  
-   Configure los valores del servicio de datos de referencia, como la configuración de la conectividad con Azure Marketplace y la administración directa de proveedores de servicios de datos de referencia de terceros.  
  
-   Configure los umbrales para la limpieza y las actividades de búsqueda de coincidencias.  
  
-   Habilite y deshabilite las notificaciones en [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)].  
  
-   Configure el registro según el nivel de gravedad de los eventos.  
  
##  <a name="AdminUsingClent"></a>Actividades de administración mediante el uso de Data Quality Client  
 Estas actividades se realizan mediante la característica de **Administración** en [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)].  
  
### <a name="activity-monitoring"></a>Supervisión de actividades  
 La pantalla de **Supervisión de actividades** en [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] muestra información detallada sobre cada actividad realizada en [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]. El administrador de datos utilizará esta pantalla principalmente para realizar una supervisión de alto nivel de todas las actividades que tienen lugar en el [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] al que está conectado la aplicación de [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] . Esta pantalla no permite realizar ninguna supervisión del sistema. Además, esta pantalla también permite a los administradores de DQS controlar una actividad o un proceso dentro de una actividad; para ello, finaliza una actividad en ejecución o detiene un proceso en ejecución dentro de una actividad, si así se necesita. Los datos se muestran para la detección del conocimiento, administración de dominios, directiva de búsqueda de coincidencias, limpieza, coincidencias y limpieza basada en SQL Server Integration Services (SSIS).  
  
### <a name="configuration"></a>Configuración  
 La pantalla de **Configuración** en [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] permite al administrador de DQS hacer lo siguiente:  
  
-   **Datos de referencia**: configuración de proveedores de servicios de datos de referencia: Azure Marketplace o proveedores de servicios de datos de referencia directos. Una vez haya establecido los proveedores de servicios de datos de referencia, podrá asignar un dominio o un dominio compuesto a los datos de referencia durante la actividad de administración de dominios en una base de conocimiento y, posteriormente, usar la misma base de conocimiento para la actividad de limpieza en un proyecto de calidad de datos. También permite especificar la configuración de proxy para conectarse a Internet para usar Azure Marketplace.  
  
-   **Configuración general**: especifique los valores de umbral para la limpieza de datos y la coincidencia de datos, y si desea habilitar las notificaciones para la generación de perfiles en [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]. Estos umbrales los utiliza DQS durante la limpieza asistida por PC y las actividades de búsqueda de coincidencias en un proyecto de calidad de datos.  
  
-   **Configuración de registro**: los archivos de registro de DQS registran las actividades realizadas en DQS y son útiles para realizar el seguimiento de los problemas operativos durante el mantenimiento y la solución de problemas. Puede filtrar los mensajes que desee registrar para varias características de DQS (administración de dominios, detección del conocimiento, limpieza, coincidencias y servicios de datos de referencia) y módulos de DQS según el nivel de gravedad de los eventos.  
  
> [!NOTE]  
>  La pantalla de **Configuración** solo está disponible para los usuarios que tengan el rol dqs_administrator en la base de datos de DQS_MAIN.  
  
##  <a name="AdminOutsideClient"></a>Actividades de administración fuera de Data Quality Client  
 Estas actividades se realizan fuera de Data Quality Client:  
  
-   **Copias de seguridad y restauración de bases**de datos de DQS: las copias de seguridad y restauración de bases de datos de DQS son las mismas que para realizar copias de seguridad y restaurar cualquier base de datos de SQL Server con algunas consideraciones específicas para DQS.  
  
-   **Desasociar y adjuntar bases de datos de DQS**: los pasos para separar y adjuntar bases de datos de DQS son los mismos que para separar y adjuntar cualquier base de datos de SQL Server con algunas consideraciones específicas para DQS.  
  
 Para más información, consulte [Manage DQS Databases](../../2014/data-quality-services/manage-dqs-databases.md).  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descripción de la tarea|Tema|  
|----------------------|-----------|  
|Describe cómo supervisar actividades en DQS.|[Supervisar las actividades de DQS](../../2014/data-quality-services/monitor-dqs-activities.md)|  
|Describe cómo configurar valores de datos de referencia en DQS.|[Configurar DQS para utilizar datos de referencia](../../2014/data-quality-services/configure-dqs-to-use-reference-data.md)|  
|Describe cómo configurar los umbrales para las actividades de limpieza y búsqueda de coincidencias.|[Configurar los valores de umbral para la limpieza y coincidencia](../../2014/data-quality-services/configure-threshold-values-for-cleansing-and-matching.md)|  
|Describe cómo habilitar o deshabilitar las notificaciones en DQS.|[Habilitar o deshabilitar notificaciones de generación de perfiles en DQS](../../2014/data-quality-services/enable-or-disable-profiling-notifications-in-dqs.md)|  
|Describe cómo configurar el registro de DQS basado en el nivel de gravedad de los eventos.|[Configurar los niveles de gravedad de los archivos de registro de DQS](../../2014/data-quality-services/configure-severity-levels-for-dqs-log-files.md)|  
|Describe cómo configurar las configuraciones avanzadas del registro de DQS.|[Configurar las opciones avanzadas de los archivos de registro de DQS](../../2014/data-quality-services/configure-advanced-settings-for-dqs-log-files.md)|  
|Describe cómo realizar copias de seguridad y restaurar bases de datos de DQS.|[Realizar copias de seguridad de bases de datos de DQS y restaurarlas](../../2014/data-quality-services/backing-up-and-restoring-dqs-databases.md)|  
|Describe cómo adjuntar y separar bases de datos de DQS.|[Separar y adjuntar bases de datos de DQS](../../2014/data-quality-services/detaching-and-attaching-dqs-databases.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Data Services de referencia en DQS](../../2014/data-quality-services/reference-data-services-in-dqs.md)   
 [Administrar archivos de registro de DQS](../../2014/data-quality-services/manage-dqs-log-files.md)   
 [Manage DQS Databases](../../2014/data-quality-services/manage-dqs-databases.md)  
  
  
