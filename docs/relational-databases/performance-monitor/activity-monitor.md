---
title: Monitor de actividad | Microsoft Docs
description: Descubra cómo usar el Monitor de actividad para obtener información sobre los procesos de SQL Server y la forma en que estos procesos afectan a la instancia actual de SQL Server.
ms.custom: ''
ms.date: 04/07/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Activity Monitor [SQL Server]
ms.assetid: 1e6c430d-3a2a-468e-a3d5-ef5459c36c15
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: d634a2e790edb01747014e930e677e18a1f8b0a3
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/28/2020
ms.locfileid: "87243816"
---
# <a name="activity-monitor"></a>Monitor de actividad
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
El Monitor de actividad muestra información acerca de los procesos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y el modo en que estos afectan a la instancia actual de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Monitor de actividad es una ventana de documento con pestañas con los paneles siguientes que se pueden expandir y contraer: **Introducción**, **Procesos**, **Esperas de recursos**, **E/S de archivo de datos**, **Consultas costosas recientes** y **Consultas costosas activas**. Cuando un panel está expandido, el Monitor de actividad consulta la instancia en busca de información. Si el panel está contraído, cualquier actividad de consulta se detiene en ese panel. Se pueden expandir uno o varios paneles al mismo tiempo para ver diferentes tipos de actividad de la instancia.  
 
## <a name="customize-columns"></a>Personalizar columnas 
En las columnas incluidas en los paneles **Procesos**, **Esperas de recursos**, **E/S de archivo de datos**, **Consultas costosas recientes** y **Consultas costosas activas**, se puede personalizar la presentación mediante los mecanismos siguientes:  
  
1.  Para reorganizar el orden de las columnas, haga clic en el encabezado de una columna y arrástrelo hasta otra ubicación de la cinta de opciones del encabezado.  
  
2.  Para ordenar una columna, haga clic en el nombre de la columna.  
  
3.  Para filtrar por una o varias columnas, haga clic en la flecha de lista desplegable del encabezado de columna y, a continuación, seleccione un valor.  

## <a name="more-information"></a>Más información  
   
|Descripción|Tema|  
|-|-|  
|Describe cómo abrir el Monitor de actividad y la forma en que se establece el intervalo de actualización del Monitor de actividad.|[Abrir el Monitor de actividad &#40;SQL Server Management Studio&#41;](../../relational-databases/performance-monitor/open-activity-monitor-sql-server-management-studio.md)|  
|Vínculos a temas de supervisión de la actividad y el rendimiento del servidor.|[Supervisión de la actividad y rendimiento del servidor](../../relational-databases/performance/server-performance-and-activity-monitoring.md)|  
  
  
