---
title: Creación de gráficos, alertas, registros e informes | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- System Monitor [SQL Server], charts and reports
- charts [SQL Server]
- reports [SQL Server]
- reports [SQL Server], creating
- Windows System Monitor [SQL Server], charts and reports
- logs [SQL Server], System Monitor
- System Monitor [SQL Server], logs
- Windows System Monitor [SQL Server], logs
ms.assetid: c9162b37-e5dc-43d1-a3aa-1e9ebc69fecc
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: c04ceea8c017feec6f214eaf3d9b442f98d4e18d
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85063923"
---
# <a name="create-charts-alerts-logs-and-reports"></a>Crear gráficos, alertas, registros e informes
  El Monitor de sistema le permite crear gráficos, alertas, registros e informes para supervisar una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="charts"></a>Gráficos  
 Los gráficos pueden supervisar el rendimiento actual de los objetos y contadores seleccionados; por ejemplo, el uso de la CPU o la E/S de disco. Puede agregar a un gráfico varias combinaciones de objetos y contadores del Monitor de sistema También puede agregar objetos y contadores de [!INCLUDE[msCoName](../../includes/msconame-md.md)] a un gráfico.  
  
 Cada gráfico representa un subconjunto de información que desea supervisar. Por ejemplo, mediante un gráfico puede realizar el seguimiento de las estadísticas relativas al uso de la memoria y, con otro gráfico, el seguimiento de las estadísticas relativas a la E/S de disco.  
  
 El uso de gráficos puede resultar útil para realizar las siguientes tareas:  
  
-   Investigar las causas de la lentitud o la ineficacia de equipos o aplicaciones.  
  
-   Supervisar sistemas de manera continua para buscar problemas de rendimiento intermitentes.  
  
-   Descubrir las causas de la necesidad de aumentar la capacidad.  
  
-   Mostrar una tendencia como un gráfico de líneas.  
  
-   Mostrar comparaciones en histogramas.  
  
 Los gráficos son útiles para la supervisión a corto plazo en tiempo real de equipos locales o remotos, por ejemplo, cuando se desea supervisar un evento a medida que se produce.  
  
## <a name="alerts"></a>Alertas  
 Mediante las alertas, el Monitor de sistema realiza un seguimiento de eventos específicos y le notifica dichos eventos cuando lo solicite. El registro de alertas permite supervisar el rendimiento actual de contadores e instancias seleccionados de objetos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Cuando un contador supera un valor determinado, se guardan en el registro la fecha y hora del evento. Un evento también puede generar una alerta de red. Puede establecer la ejecución de un programa específico la primera vez o cada vez que se produzca un evento. Por ejemplo, una alerta puede enviar un mensaje de red a todos los administradores del sistema acerca de que la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se está quedando sin espacio en disco.  
  
## <a name="logs"></a>Registros  
 Los registros permiten grabar información acerca de la actividad actual de objetos y equipos seleccionados para su posterior presentación y análisis. Puede recopilar datos de múltiples sistemas en un único archivo de registro. Por ejemplo, puede crear diferentes registros para acumular información acerca del rendimiento de objetos seleccionados en diversos equipos para su posterior análisis. Asimismo, puede guardar estas selecciones en un archivo y volverlas a utilizar cuando desee crear otro registro con información similar para realizar una comparación.  
  
 Los archivos de registro proporcionan una gran cantidad de información para la solución de problemas y el planeamiento. Mientras que los gráficos, alertas e informes acerca de la actividad actual proporcionan una evaluación instantánea, los archivos de registro permiten realizar un seguimiento de los contadores durante un largo período de tiempo. Por tanto, puede analizar la información más exhaustivamente y documentar el rendimiento del sistema.  
  
## <a name="reports"></a>Informes  
 Los informes permiten mostrar el cambio continuo en los valores de contadores e instancias de los objetos seleccionados. Los valores se muestran en columnas para cada instancia. Puede ajustar los intervalos de informes, imprimir instantáneas y exportar datos. Utilice informes cuando necesite mostrar los números sin procesar.  
  
 Para obtener más información acerca de la creación gráficos, alertas, registros e informes, o acerca de objetos y contadores de Windows, consulte la documentación de Windows.  
  
## <a name="see-also"></a>Consulte también  
 [Supervisar el uso de recursos&#40;Monitor de sistema&#41;](monitor-resource-usage-system-monitor.md)  
  
  
