---
title: Supervisar una visión general de la instancia de Analysis Services | Microsoft Docs
ms.date: 11/16/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1ac0f94b7f12cdba6237b2694114580f56dc6597
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52540458"
---
# <a name="monitoring-overview"></a>Información general de la supervisión
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

Analysis Services tiene varias herramientas que le ayudarán a supervisar y y optimizar el rendimiento de los servidores. La elección de la herramienta depende del tipo de supervisión u optimización que se realice y de los eventos particulares que se supervisen.

Para obtener más información sobre la supervisión de SQL Server Analysis Services, consulte el [Guía de operaciones de SQL Server 2008 R2](http://go.microsoft.com/fwlink/?LinkID=225539).  
  
## <a name="monitoring-tools"></a>Herramientas de supervisión  

|Herramienta  |Descripción  |
|---------|---------|
|[SQL Server Profiler](../../analysis-services/instances/use-sql-server-profiler-to-monitor-analysis-services.md)      |   Supervisa los eventos del proceso de motor. También captura datos sobre estos eventos, lo que le permite supervisar la actividad del servidor y base de datos.      |
| [Eventos extendidos](../../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md)     |   Un seguimiento de peso ligero y supervisión del rendimiento del sistema que usa muy pocos recursos del sistema, lo que una herramienta ideal para diagnosticar problemas en los servidores de producción y prueba.       |
| [Vistas de administración dinámica &#40;DMV&#41;](../../analysis-services/instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md)      |   Consultas que devuelven información acerca de los objetos del modelo, las operaciones del servidor y el estado del servidor. La consulta, basada en SQL, es una interfaz para los conjuntos de filas de esquema.      |
| [Los eventos de seguimiento](https://docs.microsoft.com/bi-reference/trace-events/analysis-services-trace-events)     |  Siga la actividad de una instancia mediante la captura y, a continuación, analizar los eventos de seguimiento generados por la instancia. Los eventos de seguimiento están agrupados para que pueda encontrar más fácilmente aquellos que estén relacionados.        |
|   [Contadores de rendimiento](../../analysis-services/instances/performance-counters-ssas.md)\*    |    Mediante el Monitor de rendimiento, puede supervisar el rendimiento de una instancia de Microsoft SQL Server Analysis Services (SSAS) mediante contadores de rendimiento.     |
|[Operaciones de registro](../../analysis-services/instances/performance-counters-ssas.md)\*|Una instancia de SQL Server Analysis Services registrará las notificaciones de servidor, los errores y advertencias en el archivo msmdsrv.log: uno para cada instancia que instale. |

\* Se aplica a SQL Server Analysis Services solo.

## <a name="see-also"></a>Vea también

[Supervisar las métricas del servidor de Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-monitor)   
[Configuración del registro de diagnóstico de Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-logging)
