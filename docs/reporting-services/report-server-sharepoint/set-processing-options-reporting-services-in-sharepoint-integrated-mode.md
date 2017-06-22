---
title: Establecer opciones de procesamiento (Reporting Services en modo integrado de SharePoint) | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SharePoint integration [Reporting Services], content management
- snapshots [Reporting Services], creating
ms.assetid: 453b19a1-739a-4b67-aeea-2069b52204e1
caps.latest.revision: 15
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8f2a5c52f4fa9b04026490c1e66243bf0d660c13
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="set-processing-options-reporting-services-in-sharepoint-integrated-mode"></a>Establecer opciones de procesamiento (Reporting Services en el modo integrado de SharePoint)
  Puede establecer opciones de procesamiento en un informe [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para determinar cuándo debe tener lugar el procesamiento de datos. También puede establecer un valor de tiempo de espera para el procesamiento de informes, así como opciones que determinen si debe habilitarse el historial de informes para el informe actual.  
  
-   Los informes pueden ejecutarse como una instantánea de informe si se desea evitar que el informe se ejecute de forma arbitraria (durante una copia de seguridad programada, por ejemplo). Una instantánea de informe suele crearse y actualizarse posteriormente según una programación, lo que permite controlar con exactitud el momento en que se producirá el procesamiento del informe y los datos. Si un informe se basa en consultas que tardan demasiado en ejecutarse o en consultas que usan datos desde un origen de datos al que prefiere que nadie tenga acceso durante determinadas horas, debe ejecutar el informe como instantánea.  
  
-   Un servidor de informes puede almacenar en memoria caché una copia de un informe procesado y devolverla cuando el usuario abra el informe. El almacenamiento en caché es una técnica de mejora del rendimiento. El almacenamiento en caché puede reducir el tiempo necesario para recuperar un informe cuando éste es demasiado grande o se utiliza con frecuencia.  
  
-   El historial del informe es un conjunto de copias de un informe ejecutadas con anterioridad. Puede usar el historial de informe para conservar un registro de un informe a lo largo del tiempo. El historial del informe no se ha diseñado para informes que contienen datos confidenciales o personales. Por este motivo, el historial solamente puede incluir aquellos informes que realizan una consulta a un origen de datos mediante un único conjunto de credenciales (sean credenciales almacenadas o credenciales usadas para la ejecución de informes desatendida) disponible para todos los usuarios que ejecutan un informe.  
  
    > [!NOTE]  
    >  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] con SharePoint usa las características de mantenimiento de entrada y salida de SharePoint para guardar las actualizaciones en los tipos de contenido de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Esto incluye la creación de instantáneas de informe. Por consiguiente si ha habilitado la versión en una biblioteca de documentos, verá la versión del informe actualizada cuando se crea una nueva instantánea del historial de informes. Este es un efecto secundario de actualizar las instantáneas. Cuando una instantánea está actualizada hace que la propiedad LastExecution del informe cambie y eso producirá un cambio en la versión del informe.  
  
-   La especificación de valores de tiempo de espera permite establecer límites relativos al empleo de los recursos del sistema.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] |  
  
 **En este tema:**  
  
-   [Para establecer opciones de actualización de datos](#bkmk_set_data_refresh)  
  
-   [Para establecer opciones de almacenamiento en caché de informes](#bkmk_set_report_caching)  
  
-   [Para establecer valores de tiempo de espera de procesamiento](#bkmk_set_processing)  
  
-   [Para establecer opciones y límites del historial de informes](#bkmk_set_report_history)  
  
-   [Establecer tiempo de espera de base de datos](#bkmk_set_database_timeout)  
  
##  <a name="bkmk_set_data_refresh"></a> Para establecer opciones de actualización de datos  
  
1.  Seleccione un informe en la biblioteca.  
  
2.  Haga clic en la flecha abajo y, a continuación, seleccione **Administrar opciones de procesamiento**.  
  
3.  En **Opciones de actualización de datos**, haga clic en **Usar datos de instantánea**. Si se muestra el mensaje "Este informe no se puede ejecutar desde una instantánea porque una o varias de las credenciales de los orígenes de datos no están almacenadas", significa que el informe no está configurado para ejecutarse en modo desatendido y que debe modificar los orígenes de datos para usar credenciales almacenadas antes de establecer esta opción.  
  
4.  En **Opciones de instantánea de datos**, seleccione **Programar procesamiento de datos**.  
  
5.  Seleccione **En una programación compartida** si dispone de una programación compartida que desee usar; de lo contrario, haga clic en **En una programación personalizada**y, a continuación, haga clic en **Configurar**.  
  
6.  Seleccione la frecuencia, la programación y las fechas de inicio y finalización y, a continuación, haga clic en **Aceptar**.  
  
7.  En **Opciones de instantáneas de datos**, seleccione **Crear o actualizar la instantánea cuando se guarde la página** si desea crear datos de instantáneas inmediatamente para utilizarlos con el informe, sin esperar a que tenga lugar el procesamiento de datos programados.  
  
##  <a name="bkmk_set_report_caching"></a> Para establecer opciones de almacenamiento en caché de informes  
  
1.  Seleccione un informe en la biblioteca.  
  
2.  Haga clic en la flecha abajo y, a continuación, seleccione **Administrar opciones de procesamiento**.  
  
3.  En **Opciones de actualización de datos**, haga clic en **Usar datos en caché**. Si se muestra el mensaje "No se pudo almacenar en caché el informe porque una o varias de las credenciales de orígenes de datos no están almacenadas", significa que el informe no está configurado para ejecutarse en modo desatendido y que debe modificar los orígenes de datos para usar credenciales almacenadas antes de establecer esta opción.  
  
4.  En **Opciones de caché**, especifique la forma en que expirará la caché:  
  
    -   Escriba un número de minutos tras los que expirará la caché.  
  
    -   Use una programación compartida para borrar la caché a las horas especificadas en la programación.  
  
    -   Cree una programación personalizada para borrar la caché a la hora especificada.  
  
##  <a name="bkmk_set_processing"></a> Para establecer valores de tiempo de espera de procesamiento  
  
1.  Seleccione un informe en la biblioteca.  
  
2.  Haga clic en la flecha abajo y, a continuación, seleccione **Administrar opciones de procesamiento**.  
  
3.  En **Tiempo de espera de procesamiento**, seleccione **Usar configuración predeterminada del sitio** si quiere usar el valor especificado en el nivel del servidor de informes. De lo contrario, seleccione **No agotar tiempo de espera de procesamiento de informes** o **Limitar procesamiento de informe a (en segundos)** si quiere reemplazar dicho valor por valores de tiempo de espera distintos o por ningún valor de tiempo de espera en absoluto.  
  
##  <a name="bkmk_set_report_history"></a> Para establecer opciones y límites del historial de informes  
  
1.  Seleccione un informe en la biblioteca.  
  
2.  Haga clic en la flecha abajo y, a continuación, seleccione **Administrar opciones de procesamiento**.  
  
3.  En **Opciones de instantáneas del historial**, especifique cuándo y cómo debe producirse el procesamiento y almacenamiento de los datos.  
  
4.  En **Límites de instantáneas del historial**, seleccione **Usar configuración predeterminada del sitio** si desea utilizar el valor especificado en el nivel del servidor de informes. De lo contrario, seleccione **No limitar el número de instantáneas** o **Limitar número de instantáneas a** para especificar un valor personalizado.  
  
##  <a name="bkmk_set_database_timeout"></a> Establecer tiempo de espera de base de datos  
  
1.  Usar Windows PowerShell para establecer el tiempo de espera de la base de datos de un servidor de informes de SharePoint. Para más información, vea la sección "Obtener y establecer las propiedades de la base de datos de la aplicación de servicio de generación de informes" de [PowerShell cmdlets for Reporting Services SharePoint Mode](../../reporting-services/report-server-sharepoint/powershell-cmdlets-for-reporting-services-sharepoint-mode.md).  
  
## <a name="see-also"></a>Vea también  
 [Establecer las propiedades del procesamiento de informes](../../reporting-services/report-server/set-report-processing-properties.md)   
 [Informes almacenados en caché &#40;SSRS&#41;](../../reporting-services/report-server/caching-reports-ssrs.md)   
 [Establecer valores de tiempo de espera para el procesamiento de informes y conjuntos de datos compartidos &#40;SSRS&#41;](../../reporting-services/report-server/setting-time-out-values-for-report-and-shared-dataset-processing-ssrs.md)  
  
  
