---
title: Almacenamiento proactivo en caché (dimensiones) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- dimensions [Analysis Services], proactive caching
- proactive caching [Analysis Services]
ms.assetid: 7d57fe93-6e5f-4a50-844f-dd2bbdbb94a5
caps.latest.revision: 7
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 86634be8be55ff48f2eac1a4c4453f7cdd5eddb9
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36199782"
---
# <a name="proactive-caching-dimensions"></a>Almacenamiento en caché automático (Dimensiones)
  El almacenamiento en caché automático proporciona la creación y administración automáticas de la memoria caché MOLAP para objetos OLAP. Los cubos incorporan inmediatamente los cambios que se realizan en los datos de la base de datos, basándose en las notificaciones recibidas de la base de datos. El objetivo del almacenamiento en caché automático consiste en proporcionar el rendimiento de MOLAP tradicional, a la vez que se conserva la inmediatez y la facilidad de administración que proporciona ROLAP.  
  
 Un objeto <xref:Microsoft.AnalysisServices.ProactiveCaching> simple se compone de una especificación de tiempo y una notificación de tabla. La especificación de tiempo define el horario para actualizar la caché una vez recibida una notificación de cambio. La notificación de tabla define el esquema de la notificación entre la tabla de datos y el objeto <xref:Microsoft.AnalysisServices.ProactiveCaching>.  
  
  