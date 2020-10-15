---
title: Comprobar la ejecución de un informe | Microsoft Docs
description: Aprenda a usar los archivos de registro o hacer referencia a la información de estado que se muestra con un informe para comprobar que se ejecuta en el Administrador de informes.
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- auditing [Reporting Services]
- verifying report execution
- logs [Reporting Services], verifying report run
- report execution data [Reporting Services]
- status information [Reporting Services]
- report processing [Reporting Services], verifying execution
- checking report execution
ms.assetid: 18a98f2f-6b40-454e-9b37-568ed1a96458
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 89f3381fdd26cc2fccc5aec34049e7d97fce4ef3
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/13/2020
ms.locfileid: "91987483"
---
# <a name="verifying-a-report-run"></a>Comprobar la ejecución de un informe
  Para ver información acerca del estado del procesamiento de un informe, puede utilizar los archivos de registro o bien consultar la información de estado que se muestra junto con el informe en el Administrador de informes.  
  
## <a name="sources-of-report-execution-data"></a>Orígenes de datos de ejecución de informes  
 Los registros de ejecución de los informes ofrecen información exhaustiva sobre la ejecución del informe, incluido el nombre del informe, el nombre del usuario que llevó a cabo la ejecución, la hora de ejecución y la extensión de entrega utilizada para distribuir el informe. Para ver y analizar estos datos, puede copiar el registro de ejecución del informe en tablas de base de datos, donde resulta muy sencillo consultar y estudiar los datos.  
  
 Los archivos de registro contienen muchas entradas sobre la ejecución del informe y otras actividades del servidor. Debido a la gran cantidad de datos que incluyen, quizás desee utilizar el Administrador de informes si solamente desea comprobar la última vez que se ejecutó el informe. Si desea consultar información adicional, deberá utilizar los archivos de registro.  
  
> [!NOTE]  
>  El Administrador de informes no muestra las horas de procesamiento de los informes ejecutados a petición.  
  
 En la siguiente tabla se describe cómo ver la fecha y la hora de procesamiento de distintos tipos de informes.  
  
|Para este tipo de informe|La información de fecha y hora se halla en|Para ver la información, haga lo siguiente|  
|-----------------------------|-----------------------------------------------|-----------------------------------------------|  
|Un informe que se ejecuta como una instantánea de informe.|En la página Contenido. Para más información, vea [Contenido &#40;página del Administrador de informes&#41;](/previous-versions/sql/sql-server-2016/ms186470(v=sql.130)).|1) Vaya a la carpeta que contiene el informe.<br /><br /> 2) Establezca la carpeta en la vista Detalles.<br /><br /> 3) Anote la fecha y hora indicadas en la columna **When Run** (Cuándo se ejecuta).|  
|Una instantánea del historial del informe.|En la página de propiedades Historial. Para más información, vea [Página de propiedades de opciones de instantánea &#40;Administrador de informes&#41;](/previous-versions/sql/sql-server-2016/ms189952(v=sql.130)).|1) Abra el informe.<br /><br /> 2) Haga clic en la página **Propiedades** .<br /><br /> 3) Haga clic en la pestaña **Historial** .<br /><br /> 4) Anote la fecha y hora indicadas en la columna **When Run** (Cuándo se ejecuta).|  
|Un informe en la memoria caché.|En la programación utilizada para crear y actualizar el informe en la memoria caché.|1) Abra el informe.<br /><br /> 2) Haga clic en la página **Propiedades** .<br /><br /> 3) Haga clic en la pestaña **Ejecución** .<br /><br /> 4) Abra la programación.|  
  
## <a name="see-also"></a>Consulte también  
 [Archivos de registro y orígenes de Reporting Services](../../reporting-services/report-server/reporting-services-log-files-and-sources.md)   
 [Establecer las propiedades del procesamiento de informes](../../reporting-services/report-server/set-report-processing-properties.md)   
 [Administrador de informes &#40;Modo nativo de SSRS&#41;](../web-portal-ssrs-native-mode.md)  
  
