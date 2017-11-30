---
title: Establecer opciones de procesamiento (Reporting Services en el modo integrado de SharePoint)| Microsoft Docs
ms.custom: 
ms.date: 10/05/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: be09d11f5a9fcdddc49a092c37be720dad0581c0
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="set-processing-options-reporting-services-in-sharepoint-integrated-mode"></a>Establecer opciones de procesamiento (Reporting Services en el modo integrado de SharePoint)

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

  Puede establecer opciones de procesamiento en un informe de Reporting Services para determinar cuándo debe tener lugar el procesamiento de datos. También puede establecer un valor de tiempo de espera para el procesamiento de informes, así como opciones que determinen si debe habilitarse el historial de informes para el informe actual.  
  
-   Los informes pueden ejecutarse como una instantánea de informe si se desea evitar que el informe se ejecute de forma arbitraria (durante una copia de seguridad programada, por ejemplo). Una instantánea de informe suele crearse y actualizarse posteriormente según una programación, lo que permite controlar con exactitud el momento en que se producirá el procesamiento del informe y los datos. Si un informe se basa en consultas que tardan demasiado en ejecutarse o en consultas que usan datos desde un origen de datos al que prefiere que nadie tenga acceso durante determinadas horas, debe ejecutar el informe como instantánea.  
  
-   Un servidor de informes puede almacenar en memoria caché una copia de un informe procesado y devolverla cuando el usuario abra el informe. El almacenamiento en caché es una técnica de mejora del rendimiento. El almacenamiento en caché puede reducir el tiempo necesario para recuperar un informe cuando éste es demasiado grande o se utiliza con frecuencia.  
  
-   El historial del informe es un conjunto de copias de un informe ejecutadas con anterioridad. Puede usar el historial de informe para conservar un registro de un informe a lo largo del tiempo. El historial del informe no se ha diseñado para informes que contienen datos confidenciales o personales. Por este motivo, el historial solamente puede incluir aquellos informes que realizan una consulta a un origen de datos mediante un único conjunto de credenciales (sean credenciales almacenadas o credenciales usadas para la ejecución de informes desatendida) disponible para todos los usuarios que ejecutan un informe.  

    La integración de Reporting Services con SharePoint usa las características de mantenimiento de entrada y salida de SharePoint para guardar las actualizaciones en los tipos de contenido de Reporting Services. Esto incluye la creación de instantáneas de informe. Por consiguiente si ha habilitado la versión en una biblioteca de documentos, verá la versión del informe actualizada cuando se crea una nueva instantánea del historial de informes. Este es un efecto secundario de actualizar las instantáneas. Cuando una instantánea está actualizada hace que la propiedad LastExecution del informe cambie y eso producirá un cambio en la versión del informe.  

-   La especificación de valores de tiempo de espera permite establecer límites relativos al empleo de los recursos del sistema.  

> [!NOTE]
> La integración de Reporting Services con SharePoint ya no está disponible después de SQL Server 2016.

## <a name="set-data-refresh-options"></a>Establecer opciones de actualización de datos
  
1.  Seleccione un informe en la biblioteca.  
  
2.  Haga clic en la flecha abajo y, a continuación, seleccione **Administrar opciones de procesamiento**.  
  
3.  En **Opciones de actualización de datos**, haga clic en **Usar datos de instantánea**. Si se muestra el mensaje "Este informe no se puede ejecutar desde una instantánea porque una o varias de las credenciales de los orígenes de datos no están almacenadas", significa que el informe no está configurado para ejecutarse en modo desatendido y que debe modificar los orígenes de datos para usar credenciales almacenadas antes de establecer esta opción.  
  
4.  En **Opciones de instantánea de datos**, seleccione **Programar procesamiento de datos**.  
  
5.  Seleccione **En una programación compartida** si dispone de una programación compartida que desee usar; de lo contrario, haga clic en **En una programación personalizada**y, a continuación, haga clic en **Configurar**.  
  
6.  Seleccione la frecuencia, la programación y las fechas de inicio y finalización y, a continuación, haga clic en **Aceptar**.  
  
7.  En **Opciones de instantáneas de datos**, seleccione **Crear o actualizar la instantánea cuando se guarde la página** si desea crear datos de instantáneas inmediatamente para utilizarlos con el informe, sin esperar a que tenga lugar el procesamiento de datos programados.  
  
## <a name="set-report-caching-options"></a>Establecer opciones de almacenamiento en caché de informes
  
1.  Seleccione un informe en la biblioteca.  
  
2.  Haga clic en la flecha abajo y, a continuación, seleccione **Administrar opciones de procesamiento**.  
  
3.  En **Opciones de actualización de datos**, haga clic en **Usar datos en caché**. Si se muestra el mensaje "No se pudo almacenar en caché el informe porque una o varias de las credenciales de orígenes de datos no están almacenadas", significa que el informe no está configurado para ejecutarse en modo desatendido y que debe modificar los orígenes de datos para usar credenciales almacenadas antes de establecer esta opción.  
  
4.  En **Opciones de caché**, especifique la forma en que expirará la caché:  
  
    -   Escriba un número de minutos tras los que expirará la caché.  
  
    -   Use una programación compartida para borrar la caché a las horas especificadas en la programación.  
  
    -   Cree una programación personalizada para borrar la caché a la hora especificada.  
  
## <a name="set-processing-time-out-values"></a>Establecer valores de tiempo de espera de procesamiento
  
1.  Seleccione un informe en la biblioteca.  
  
2.  Haga clic en la flecha abajo y, a continuación, seleccione **Administrar opciones de procesamiento**.  
  
3.  En **Tiempo de espera de procesamiento**, seleccione **Usar configuración predeterminada del sitio** si quiere usar el valor especificado en el nivel del servidor de informes. De lo contrario, seleccione **No agotar tiempo de espera de procesamiento de informes** o **Limitar procesamiento de informe a (en segundos)** si quiere reemplazar dicho valor por valores de tiempo de espera distintos o por ningún valor de tiempo de espera en absoluto.  
  
## <a name="set-report-history-options-and-limits"></a>Establecer opciones y límites del servidor de informes
  
1.  Seleccione un informe en la biblioteca.  
  
2.  Haga clic en la flecha abajo y, a continuación, seleccione **Administrar opciones de procesamiento**.  
  
3.  En **Opciones de instantáneas del historial**, especifique cuándo y cómo debe producirse el procesamiento y almacenamiento de los datos.  
  
4.  En **Límites de instantáneas del historial**, seleccione **Usar configuración predeterminada del sitio** si desea utilizar el valor especificado en el nivel del servidor de informes. De lo contrario, seleccione **No limitar el número de instantáneas** o **Limitar número de instantáneas a** para especificar un valor personalizado.  
  
## <a name="set-database-timeout"></a>Establecer tiempo de espera de base de datos
  
*  Usar Windows PowerShell para establecer el tiempo de espera de la base de datos de un servidor de informes de SharePoint. Para más información, vea la sección "Obtener y establecer las propiedades de la base de datos de la aplicación de servicio de generación de informes" de [PowerShell cmdlets for Reporting Services SharePoint Mode](../../reporting-services/report-server-sharepoint/powershell-cmdlets-for-reporting-services-sharepoint-mode.md).  
  
## <a name="next-steps"></a>Pasos siguientes

 [Establecer las propiedades del procesamiento de informes](../../reporting-services/report-server/set-report-processing-properties.md)   
 [Informes almacenados en caché](../../reporting-services/report-server/caching-reports-ssrs.md)   
 [Establecer valores de tiempo de espera para el procesamiento de informes y conjuntos de datos compartidos](../../reporting-services/report-server/setting-time-out-values-for-report-and-shared-dataset-processing-ssrs.md)  

¿Tiene alguna pregunta más? [Puede plantear sus dudas en el foro de Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231).
