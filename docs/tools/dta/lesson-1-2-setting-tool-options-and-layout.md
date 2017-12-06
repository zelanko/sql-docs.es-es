---
title: "Establecer opciones de herramienta y el diseño | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: dta
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-query-tuning
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
helpviewer_keywords: Database Engine [SQL Server], tutorials
ms.assetid: 43e97ce0-97bc-4a27-9485-5bbeb7190b85
caps.latest.revision: "24"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8d497ec1f8b0d7c557c6d802328ddbbb4360a988
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/05/2017
---
# <a name="lesson-1-2---setting-tool-options-and-layout"></a>Lección 1-2-opciones de la herramienta de configuración y diseño
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Puede establecer opciones que permiten configurar lo que mostrará la interfaz gráfica de usuario de Asistente para la optimización de motor de base de datos (GUI) durante el inicio, las fuentes utilizadas, y otras funciones para ofrecer la mejor cómo utilizarlo. Las prácticas de esta página le permitirán familiarizarse con las opciones que puede configurar y el modo de hacerlo.  
  
### <a name="set-the-tool-options"></a>Configurar las opciones de herramienta  
  
1.  Inicie el Asistente para la optimización de motor de base de datos. En el menú **Inicio** de Windows, elija **Todos los programas**, [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]y **Herramientas de rendimiento**, y haga clic en **Asistente para la optimización de motor de base de datos**.  
  
2.  En el menú **Herramientas** , haga clic en **Opciones**.  
  
3.  En el cuadro de diálogo **Opciones** , observe las opciones siguientes:  
  
    -   Expanda la lista **Al iniciar** para ver lo que muestra el Asistente para la optimización de motor de base de datos cuando se inicia. De forma predeterminada, está seleccionada la opción **Mostrar una nueva sesión** .  
  
    -   Haga clic en **Cambiar fuente** para ver las fuentes que puede elegir para las listas de bases de datos y tablas en la pestaña **General** . Las fuentes que elija para esta opción también se utilizarán en las cuadrículas de recomendación y los informes del Asistente para la optimización de motor de base de datos después de realizar la optimización. De forma predeterminada, el asistente utiliza las fuentes del sistema.  
  
    -   La opción **Número de elementos en las listas usadas más recientemente** puede establecerse entre **1** y **10**. De esta manera, se establece el número máximo de elementos en las listas que se muestran cuando hace clic en **Sesiones recientes** o **Archivos recientes** del menú **Archivo** . De forma predeterminada, el valor de esta opción es **4**.  
  
    -   Cuando la opción **Recordar mis últimas opciones de optimización** está activada, el Asistente para la optimización de motor de base de datos utiliza de forma predeterminada las opciones de optimización que especificó en la última sesión de optimización y las aplica a la sesión actual. Desactive esta casilla para utilizar las opciones de optimización predeterminadas del asistente. Esta opción está seleccionada de forma predeterminada.  
  
    -   La opción **Preguntar antes de eliminar permanentemente las sesiones** está activada de forma predeterminada para impedir la eliminación accidental de sesiones de optimización.  
  
    -   La opción **Preguntar antes de detener análisis de sesión** está activada de forma predeterminada para impedir la detención accidental de la sesión de optimización antes de que el Asistente para la optimización de motor de base de datos haya terminado de analizar la carga de trabajo.  
  
## <a name="next-lesson"></a>Lección siguiente  
[Lección 2: Usar el Asistente para la optimización de motor de base de datos](../../tools/dta/lesson-2-using-database-engine-tuning-advisor.md)  
  
  
  
