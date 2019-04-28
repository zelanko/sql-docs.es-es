---
title: Caché automático (dimensiones) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6f5e6bab81e982adbf8ee443bd84a5e806b960db
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62727303"
---
# <a name="proactive-caching-dimensions"></a>Almacenamiento en caché automático (Dimensiones)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  El almacenamiento en caché automático proporciona la creación y administración automáticas de la memoria caché MOLAP para objetos OLAP. Los cubos incorporan inmediatamente los cambios que se realizan en los datos de la base de datos, basándose en las notificaciones recibidas de la base de datos. El objetivo del almacenamiento en caché automático consiste en proporcionar el rendimiento de MOLAP tradicional, a la vez que se conserva la inmediatez y la facilidad de administración que proporciona ROLAP.  
  
 Un objeto <xref:Microsoft.AnalysisServices.ProactiveCaching> simple se compone de una especificación de tiempo y una notificación de tabla. La especificación de tiempo define el horario para actualizar la caché una vez recibida una notificación de cambio. La notificación de tabla define el esquema de la notificación entre la tabla de datos y el objeto <xref:Microsoft.AnalysisServices.ProactiveCaching>.  
  
  
