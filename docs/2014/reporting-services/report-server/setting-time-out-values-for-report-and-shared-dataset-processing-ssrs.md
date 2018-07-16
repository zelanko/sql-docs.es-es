---
title: Establecer valores de tiempo de espera para el procesamiento de informes y conjuntos de datos compartidos (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- time-outs [Reporting Services]
- query time-outs [Reporting Services]
- report processing [Reporting Services], time-outs
- report execution time-outs [Reporting Services]
ms.assetid: 0f9dc61d-d03c-4bbf-8090-7a53844350f8
caps.latest.revision: 38
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 4794c4a2b6c9207cb48573bb481499fa402f3b29
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37214575"
---
# <a name="setting-time-out-values-for-report-and-shared-dataset-processing-ssrs"></a>Establecer valores de tiempo de espera para el procesamiento de informes y conjuntos de datos compartidos (SSRS)
  La especificación de valores de tiempo de espera permite establecer límites relativos al empleo de los recursos del sistema. El servidor de informes admite dos valores de tiempo de espera:  
  
-   Un valor de tiempo de espera de consulta de un conjunto de datos incrustado es el número de segundos durante los que el servidor de informes espera una respuesta de la base de datos. Este valor se define en el informe.  
  
-   Un valor de tiempo de espera de consulta de un conjunto de datos compartido es el número de segundos durante los que el servidor de informes espera una respuesta de la base de datos. Este valor es parte de la definición del conjunto de datos compartido y se puede cambiar al administrar el conjunto de datos compartido en el servidor de informes.  
  
-   Un valor de tiempo de espera de informe es el número máximo de segundos durante los cuales puede continuar el procesamiento del informe antes de que se detenga. Este valor se define en el nivel de sistema. Existe la posibilidad de modificarlo para informes individuales.  
  
 La mayoría de los errores de tiempo de espera se generan durante el procesamiento de las consultas. Si detecta errores de este tipo, intente aumentar el valor de tiempo de espera de la consulta. Asegúrese de ajustar el valor de tiempo de espera de ejecución del informe de forma que sea superior al de la consulta. El período de tiempo debería ser suficiente para completar el procesamiento tanto de la consulta como del informe.  
  
## <a name="setting-a-query-time-out-for-an-embedded-dataset-in-a-report"></a>Establecer un tiempo de espera de la consulta para un conjunto de datos incrustados en un informe  
 Los valores de tiempo de espera de la consulta se especifican durante la creación del informe como un conjunto de datos incrustado. El valor de tiempo de espera se almacena con el informe, en el `Timeout` elementos de la definición de informe. De forma predeterminada, este valor está establecido en 30 segundos. Para más información, vea [Conjuntos de datos incrustados y compartidos de informe &#40;Generador de informes y SSRS&#41;](../report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md).  
  
 Los usuarios con permisos para modificar las propiedades de un informe publicado pueden restablecer este valor mediante la edición del archivo de definición del informe.  
  
 También se puede especificar un valor de tiempo de espera de consulta para las suscripciones controladas por datos. Este valor se especifica en las páginas Suscripción controlada por datos. El valor que se define determina el tiempo que esperará el servidor de informes a que se complete el procesamiento de una consulta cuando se recuperan datos del origen de datos de suscriptores.  
  
## <a name="setting-a-query-time-out-for-a-shared-dataset"></a>Establecer un tiempo de espera de la consulta para un conjunto de datos compartido  
 Los valores de tiempo de espera de la consulta se especifican en segundos en el servidor de informes al crear o administrar un conjunto de datos compartido. De forma predeterminada, este valor está establecido en 0 segundos, que equivalen a no asignar ningún valor de tiempo de espera. Para obtener más información, consulte [administrar conjuntos de datos compartidos](../report-data/manage-shared-datasets.md).  
  
## <a name="setting-a-report-execution-time-out"></a>Establecer un valor de tiempo de espera de informe  
 El valor de tiempo de espera de ejecución del informe permite limitar el tiempo que emplea un servidor de informes en procesar un informe. Los valores de tiempo de espera de ejecución del informe pueden especificarse desde el Administrador de informes. También existe la posibilidad de establecer un valor predeterminado para todos los informes desde la página Configuración del sitio, y reemplazarlo posteriormente desde la página de propiedades Ejecución para un informe específico. De forma predeterminada, este valor está establecido en 1.800 segundos. Para más información, vea [Establecer las propiedades del procesamiento de informes](set-report-processing-properties.md).  
  
## <a name="how-report-execution-time-out-values-are-evaluated"></a>Evaluar los valores de tiempo de espera de ejecución del informe  
 El servidor de informes evalúa los trabajos en ejecución a intervalos de 60 segundos. En cada intervalo, el servidor de informes compara el tiempo de procesamiento real con el valor de tiempo de espera de ejecución para el informe. El proceso se detendrá si el tiempo de procesamiento de un informe es superior al valor de tiempo de espera de ejecución del informe.  
  
 Es importante mencionar que, si se especifica un valor de tiempo de espera inferior a 60 segundos, el informe puede llegar a procesarse por completo si el proceso empieza y termina durante la parte silenciosa del ciclo en la que el servidor de informes no evalúa los trabajos en ejecución Por ejemplo, si se establece un valor de tiempo de espera de 10 segundos para un informe que necesita 20 para ejecutarse, el procesamiento del informe solamente podrá completarse si la ejecución da comienzo nada más empezar el ciclo de 60 segundos.  
  
> [!NOTE]  
>  Es posible establecer el parámetro `RunningRequestsDbCycle` del archivo RSReportServer.config para cambiar la frecuencia con la que se evalúan los trabajos en ejecución.  
  
## <a name="see-also"></a>Vea también  
 [Establecer opciones de procesamiento &#40;modo integrado de Reporting Services en SharePoint&#41;](../set-processing-options-reporting-services-in-sharepoint-integrated-mode.md)   
 [Servidor de informes de Reporting Services &#40;modo nativo&#41;](reporting-services-report-server-native-mode.md)   
 [Administrar un proceso en ejecución](../subscriptions/manage-a-running-process.md)   
 [Administrador de informes &#40;Modo nativo de SSRS&#41;](../report-manager-ssrs-native-mode.md)  
  
  
