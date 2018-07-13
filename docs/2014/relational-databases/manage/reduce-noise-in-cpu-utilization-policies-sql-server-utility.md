---
title: Reducción del ruido en las directivas de uso de la CPU (utilidad de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.SWB.UE.ReduceNoise.F1
ms.assetid: 94bf4d93-c0ff-4869-bde7-80c24866092e
caps.latest.revision: 6
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 9eb5dc31c0eb7534788b8b7e50831d0f7fa2a777
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37193105"
---
# <a name="reduce-noise-in-cpu-utilization-policies-sql-server-utility"></a>Reducir el ruido en las directivas de uso de la CPU (utilidad de SQL Server)
  Use las siguientes estrategias para reducir ruido del informe de errores y las infracciones no deseadas en las directivas de uso de los recursos de la Utilidad [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="how-frequently-should-processor-utilization-be-in-violation-before-it-is-reported-as-overutilized"></a>¿Cuántas infracciones debe cometer el procesador para que se notifique como sobreutilizado?  
 El período de tiempo de la evaluación y la tolerancia para el porcentaje de infracciones son ambos configurables usando los valores de la pestaña **Directiva** del nodo **Administración de la utilidad** del explorador de la utilidad. Para cambiar las directivas, utilice los controles deslizantes a la derecha de las descripciones de la directiva y, a continuación, haga clic en **Aplicar**. También puede restaurar los valores predeterminados o descartar los cambios con los botones en la parte inferior de la pantalla.  
  
-   El intervalo de la recopilación de datos es 15 minutos. Este valor no es configurable.  
  
-   La directiva de uso del procesador tiene un umbral superior predeterminado del 70%. Las opciones van de 0% a 100%.  
  
-   El período de evaluación predeterminado para la sobreutilización del procesador es 1 hora. Las opciones van de 1 hora a 1 semana.  
  
-   El porcentaje predeterminado de puntos de datos en infracción antes de que se notifique la sobreutilización de la CPU es del 20%. Las opciones van de 0% a 100%.  
  
 Por ejemplo, de acuerdo con los valores predeterminados, se recogerán 4 puntos de datos cada hora y el umbral de la directiva es del 20%. Así, de forma predeterminada, cualquier infracción en un período de recopilación de 1 hora será del 25% de 4 puntos de datos. Los valores predeterminado notifican cualquier infracción del umbral de la directiva de sobreutilización de la CPU.  
  
 Para reducir ruido generado por una infracción única, considere las siguientes opciones:  
  
-   Aumente el período de evaluación en 1 incremento de 6 horas. Una infracción única en 6 horas sería 1 punto de datos en un tamaño de prueba de 24. En este caso, la directiva toleraría 4 infracciones del umbral de la directiva (16,7% de puntos de datos) en 6 horas, pero notificaría la sobreutilización para 5 o más infracciones (>20% de puntos de datos) en un período de la recopilación de 6 horas.  
  
-   Aumente la tolerancia para el porcentaje de infracciones en 1 incremento del 30%. Una infracción única en 1 hora sería 1 punto de datos en un tamaño de prueba de 4. En este caso, la directiva toleraría 1 infracción por hora pero notificaría la sobreutilización para 2 o más infracciones (>30% de puntos de datos) en un período de la recopilación de 1 hora.  
  
-   Aumente los umbrales de la directiva para el uso de procesador de la instancia administrada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y la aplicación de capa de datos. Para obtener más información sobre cómo cambiar las directivas globales del uso de la CPU para las instancias administradas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o las aplicaciones de capa de datos, vea [Administración de la utilidad &#40;utilidad de SQL Server&#41;](../../database-engine/utility-administration-sql-server-utility.md). Para obtener más información sobre cómo cambiar las directivas individuales del uso de la CPU para las instancias administradas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Detalles de las instancias administradas &#40;Utilidad de SQL Server&#41;](../../database-engine/managed-instance-details-sql-server-utility.md). Para obtener más información sobre cómo cambiar las directivas de uso de la CPU de aplicaciones individuales de capa de datos, vea [Detalles de la aplicación de capa de datos implementada &#40;Utilidad de SQL Server&#41;](../../database-engine/deployed-data-tier-application-details-sql-server-utility.md).  
  
## <a name="how-frequently-should-processor-utilization-be-in-violation-before-it-is-reported-as-underutilized"></a>¿Cuántas infracciones debe cometer el procesador para que se notifique como infrautilizado?  
 El período de tiempo de la evaluación y la tolerancia para el porcentaje de infracciones son ambos configurables usando los valores de la pestaña **Directiva** del nodo **Administración de la utilidad** del explorador de la utilidad. Para cambiar las directivas, utilice los controles deslizantes a la derecha de las descripciones de la directiva y, a continuación, haga clic en **Aplicar**. También puede restaurar los valores predeterminados o descartar los cambios con los botones en la parte inferior de la pantalla.  
  
-   El intervalo de la recopilación de datos es 15 minutos. Este valor no es configurable.  
  
-   La directiva de uso del procesador tiene un umbral inferior predeterminado del 0%. Las opciones van de 0% a 100%.  
  
-   El período de evaluación predeterminado para la infrautilización del procesador es 1 semana. Las opciones van de 1 día a 1 mes.  
  
-   El porcentaje predeterminado de puntos de datos en infracción antes de que se notifique la infrautilización de la CPU es del 90%. Las opciones van de 0% a 100%.  
  
 De acuerdo con los valores predeterminados, se recogen 672 puntos cada semana, pero el umbral de la directiva es 0%. Así, de forma predeterminada, esta directiva no genera infracciones de infrautilización del procesador. Para obtener más información sobre cómo cambiar las directivas globales del uso de la CPU para las instancias administradas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o las aplicaciones de capa de datos, vea [Administración de la utilidad &#40;utilidad de SQL Server&#41;](../../database-engine/utility-administration-sql-server-utility.md). Para obtener más información sobre cómo cambiar las directivas individuales de uso de la CPU para las instancias administradas de SQL Server, vea [Detalles de las instancias administradas &#40;Utilidad de SQL Server&#41;](../../database-engine/managed-instance-details-sql-server-utility.md). Para obtener más información sobre cómo cambiar las directivas de uso de la CPU de aplicaciones individuales de capa de datos, vea [Detalles de la aplicación de capa de datos implementada &#40;Utilidad de SQL Server&#41;](../../database-engine/deployed-data-tier-application-details-sql-server-utility.md).  
  
## <a name="see-also"></a>Vea también  
 [Administración de la utilidad &#40;Utilidad de SQL Server&#41;](../../database-engine/utility-administration-sql-server-utility.md)   
 [Supervisar instancias de SQL Server en la utilidad de SQL Server](monitor-instances-of-sql-server-in-the-sql-server-utility.md)   
 [Modificar una definición de la directiva de mantenimiento de recursos &#40;Utilidad de SQL Server&#41;](modify-a-resource-health-policy-definition-sql-server-utility.md)   
 [Características y tareas de la utilidad de SQL Server](sql-server-utility-features-and-tasks.md)  
  
  
