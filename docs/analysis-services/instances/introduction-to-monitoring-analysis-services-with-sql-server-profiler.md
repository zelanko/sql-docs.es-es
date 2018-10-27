---
title: Introducción a la supervisión de Analysis Services con SQL Server Profiler | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ebae2156d1c0cc7c3459c5083723368c66d87b9e
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/26/2018
ms.locfileid: "50144702"
---
# <a name="introduction-to-monitoring-analysis-services-with-sql-server-profiler"></a>Introducción a Supervisar Analysis Services con SQL Server Profiler
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  Puede usar [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para supervisar eventos generados por una instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Mediante el [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], puede hacer lo siguiente:  
  
-   Supervisar el rendimiento de una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
-   Depurar instrucciones de expresiones multidimensionales (MDX).  
  
-   Identificar instrucciones MDX que se ejecutan lentamente.  
  
-   Probar instrucciones MDX en la fase de desarrollo de un proyecto mediante la ejecución paso a paso de las instrucciones para confirmar que el código funciona correctamente.  
  
-   Solucionar problemas de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] mediante la captura de eventos en un sistema de producción y su reproducción en un sistema de prueba. Este enfoque es útil para realizar pruebas o depuración, y permite a los usuarios seguir utilizando el sistema de producción sin interferencias.  
  
-   Auditar y revisar la actividad producida en una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Un administrador de seguridad puede revisar cualquiera de los eventos auditados. Esto incluye el éxito o fracaso de un intento de inicio de sesión y el éxito o fracaso de los permisos para tener acceso a instrucciones y objetos.  
  
-   Mostrar datos sobre los eventos capturados en la pantalla, o capturar y guardar datos sobre cada evento en un archivo o tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para un futuro análisis o reproducción. Cuando reproduzca los datos, puede volver a ejecutar los eventos guardados tal como se produjeron originalmente, en tiempo real o paso a paso.  
  
## <a name="using-sql-server-profiler"></a>Usar SQL Server Profiler  
 Para usar el [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] con el fin de crear o reproducir seguimientos, debe ser miembro del rol de servidor de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Si es miembro del rol de servidor de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , puede iniciar el [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] desde el grupo de programas de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el menú **Inicio** .  
  
 Cuando utilice el [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], tenga en cuenta lo siguiente:  
  
-   Las definiciones de seguimiento se almacenan con la base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] mediante la instrucción CREATE.  
  
-   Pueden ejecutarse varios seguimientos a la vez.  
  
-   Varias conexiones pueden recibir eventos del mismo seguimiento.  
  
-   Un seguimiento puede continuar cuando [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] se detenga y se reinicie.  
  
    > [!NOTE]  
    >  Las contraseñas no se muestran en los eventos de seguimiento, pero se reemplazan por ****** en el evento.  
  
 Con el fin de obtener un rendimiento óptimo, utilice él [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para supervisar solamente aquellos eventos en los que esté más interesado. La supervisión de demasiados eventos agrega carga y puede hacer que el archivo de seguimiento o la tabla se vuelvan muy grandes, sobre todo al supervisar un período largo de tiempo. Además, utilice filtros para limitar la cantidad de datos recopilados y para evitar que los seguimientos se vuelvan demasiado grandes.  
  
## <a name="see-also"></a>Vea también  
 [Eventos de seguimiento de Analysis Services](https://docs.microsoft.com/bi-reference/trace-events/analysis-services-trace-events)   
 [Crear seguimientos del generador de perfiles para su reproducción &#40;Analysis Services&#41;](../../analysis-services/instances/create-profiler-traces-for-replay-analysis-services.md)  
  
  
