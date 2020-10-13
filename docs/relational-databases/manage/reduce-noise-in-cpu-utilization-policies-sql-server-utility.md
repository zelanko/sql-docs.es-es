---
title: Reducción del ruido en las directivas de uso de la CPU (utilidad de SQL Server) | Microsoft Docs
description: Vea estrategias para reducir el ruido y las infracciones no deseadas en los resultados de Utilidad de SQL Server. Vea qué opciones de directiva afectan a los informes de uso del procesador.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.SWB.UE.ReduceNoise.F1
ms.assetid: 94bf4d93-c0ff-4869-bde7-80c24866092e
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 97e37ced535863dfe232fb1299be70774643c1c7
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/07/2020
ms.locfileid: "91811055"
---
# <a name="reduce-noise-in-cpu-utilization-policies-sql-server-utility"></a>Reducir el ruido en las directivas de uso de la CPU (utilidad de SQL Server)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
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
  
-   Aumente los umbrales de la directiva para el uso de procesador de la instancia administrada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y la aplicación de capa de datos. Para obtener más información sobre cómo cambiar las directivas globales del uso de la CPU para las instancias administradas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o las aplicaciones de capa de datos, vea [Administración de la utilidad &#40;Utilidad de SQL Server&#41;](/previous-versions/sql/sql-server-2016/ee240832(v=sql.130)). Para obtener más información sobre cómo cambiar las directivas individuales del uso de la CPU para las instancias administradas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Detalles de las instancias administradas &#40;Utilidad de SQL Server&#41;](./utility-explorer-f1-help.md). Para obtener más información sobre cómo cambiar las directivas de uso de la CPU de aplicaciones individuales de capa de datos, vea [Detalles de la aplicación de capa de datos implementada &#40;Utilidad de SQL Server&#41;](/previous-versions/sql/sql-server-2016/ee240857(v=sql.130)).  
  
## <a name="how-frequently-should-processor-utilization-be-in-violation-before-it-is-reported-as-underutilized"></a>¿Cuántas infracciones debe cometer el procesador para que se notifique como infrautilizado?  
 El período de tiempo de la evaluación y la tolerancia para el porcentaje de infracciones son ambos configurables usando los valores de la pestaña **Directiva** del nodo **Administración de la utilidad** del explorador de la utilidad. Para cambiar las directivas, utilice los controles deslizantes a la derecha de las descripciones de la directiva y, a continuación, haga clic en **Aplicar**. También puede restaurar los valores predeterminados o descartar los cambios con los botones en la parte inferior de la pantalla.  
  
-   El intervalo de la recopilación de datos es 15 minutos. Este valor no es configurable.  
  
-   La directiva de uso del procesador tiene un umbral inferior predeterminado del 0%. Las opciones van de 0% a 100%.  
  
-   El período de evaluación predeterminado para la infrautilización del procesador es 1 semana. Las opciones van de 1 día a 1 mes.  
  
-   El porcentaje predeterminado de puntos de datos en infracción antes de que se notifique la infrautilización de la CPU es del 90%. Las opciones van de 0% a 100%.  
  
 De acuerdo con los valores predeterminados, se recogen 672 puntos cada semana, pero el umbral de la directiva es 0%. Así, de forma predeterminada, esta directiva no genera infracciones de infrautilización del procesador. Para obtener más información sobre cómo cambiar las directivas globales del uso de la CPU para las instancias administradas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o las aplicaciones de capa de datos, vea [Administración de la utilidad &#40;Utilidad de SQL Server&#41;](/previous-versions/sql/sql-server-2016/ee240832(v=sql.130)). Para obtener más información sobre cómo cambiar las directivas individuales de uso de la CPU para las instancias administradas de SQL Server, vea [Detalles de las instancias administradas &#40;Utilidad de SQL Server&#41;](./utility-explorer-f1-help.md). Para obtener más información sobre cómo cambiar las directivas de uso de la CPU de aplicaciones individuales de capa de datos, vea [Detalles de la aplicación de capa de datos implementada &#40;Utilidad de SQL Server&#41;](/previous-versions/sql/sql-server-2016/ee240857(v=sql.130)).  
  
## <a name="see-also"></a>Consulte también  
 [Administración de la utilidad &#40;Utilidad de SQL Server&#41;](/previous-versions/sql/sql-server-2016/ee240832(v=sql.130))   
 [Supervisar instancias de SQL Server en la utilidad de SQL Server](../../relational-databases/manage/monitor-instances-of-sql-server-in-the-sql-server-utility.md)   
 [Modificar una definición de la directiva de mantenimiento de recursos &#40;Utilidad de SQL Server&#41;](../../relational-databases/manage/modify-a-resource-health-policy-definition-sql-server-utility.md)   
 [Características y tareas de la utilidad de SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)  
  
