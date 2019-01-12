---
title: Compatibilidad con versiones anteriores de SQL Server 2017 Analysis Services | Microsoft Docs
ms.date: 01/09/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 411fa78bada76c79d4a869d68c94abf752b8466a
ms.sourcegitcommit: 1c01af5b02fe185fd60718cc289829426dc86eaa
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/10/2019
ms.locfileid: "54185081"
---
# <a name="analysis-services-backward-compatibility-sql-2017"></a>Compatibilidad con versiones anteriores de Analysis Services (SQL 2017)
[!INCLUDE[ssas-appliesto-sql2017](../includes/ssas-appliesto-sql2017.md)]

En este artículo se describe los cambios en la disponibilidad de las características y el comportamiento entre la versión actual y la versión anterior.

## <a name="deprecated-features"></a>Características en desuso
Un *característica en desuso* dejará de incluirse del producto en una versión futura, pero se admite e incluida en la versión actual para mantener la compatibilidad con versiones anteriores todavía. Se recomienda que dejar de usar las características en desuso en proyectos nuevos y existentes para mantener la compatibilidad con versiones futuras. No se actualiza la documentación de características en desuso.

Las siguientes características están en desuso en esta versión:
  
|||  
|-|-|  
|**Modo o la categoría**|**Característica**|
|Multidimensional|Minería de datos|
|Multidimensional|Grupos de medida vinculados remotos|
|Tabular|Modelos en el nivel de compatibilidad 1100 y 1103|
|Tabular|Propiedades del modelo de objetos tabulares: Column.IsDefaultImage Column.TableDetailPosition, Column.IsDefaultLabel,|
|Herramientas|SQL Server Profiler para captura de seguimiento<br /><br /> La sustitución es usar el Generador de perfiles de eventos extendidos integrado en SQL Server Management Studio.  <br /> Consulte [Monitor Analysis Services with SQL Server Extended Events](../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md).|  
|Herramientas|Server Profiler para reproducción de seguimiento <br />Sustitución. No hay ninguna sustitución.|  
|Objetos de administración de seguimiento y API de seguimiento|Objetos de Microsoft.AnalysisServices.Trace (contiene las API para los objetos Trace y Replay de Analysis Services). La sustitución abarca varias partes:<br /><br /> -Configuración de seguimiento: Microsoft.SqlServer.Management.XEvent<br />-Lectura de seguimiento: Microsoft.SqlServer.XEvent.Linq<br />-Reproducción de seguimiento: None|  


## <a name="discontinued-features"></a>Características no incluidas
Un *no incluye la característica* ha quedado en desuso en una versión anterior. Puede continuar para incluirse en la versión actual, pero ya no se admite. Se pueden quitar características no incluidas en una futura versión completamente o actualizar.

Las siguientes características han quedado en desuso en una versión anterior y ya no se admiten en esta versión.
  
|||  
|-|-|  
|**Modo o la categoría**|**Característica**|  
|Tabular|Valor de propiedad de VertipaqPagingPolicy memoria (2), habilite la paginación en el disco mediante la memoria archivos asignados.|
|Multidimensional|Particiones remotas|  
|Multidimensional|Grupos de medida vinculados remotos|  
|Multidimensional|Reescritura de dimensiones|  
|Multidimensional|Dimensiones vinculadas|


## <a name="breaking-changes"></a>Cambios importantes
Un *cambio brusco* hace que una característica, modelo de datos, código de la aplicación o script ya no funcione después de actualizar a la versión actual.

No hay ningún cambio importante en esta versión.

## <a name="behavior-changes"></a>Cambios de comportamiento
Un *cambio de comportamiento* afecta a cómo funciona la misma función en la versión actual en comparación con la versión anterior. Se describen solo los cambios de comportamiento importante. No se incluyen los cambios en la interfaz de usuario.

Los cambios realizados en MDSCHEMA_MEASUREGROUP_DIMENSIONS y DISCOVER_CALC_DEPENDENCY, se detallan en el [Novedades de SQL Server 2017 CTP 2.1 para Analysis Services](https://blogs.msdn.microsoft.com/analysisservices/2017/05/18/whats-new-in-sql-server-2017-ctp-2-1-for-analysis-services/) anuncio.


## <a name="see-also"></a>Vea también
[Compatibilidad con versiones anteriores de Analysis Services (SQL Server 2016)](analysis-services-backward-compatibility.md)
