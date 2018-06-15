---
title: Establecer opciones de herramienta y el diseño | Documentos de Microsoft
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: dta
ms.reviewer: ''
ms.suite: sql
ms.technology: performance
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- SQL Server 2016
helpviewer_keywords:
- Database Engine [SQL Server], tutorials
ms.assetid: 43e97ce0-97bc-4a27-9485-5bbeb7190b85
caps.latest.revision: 24
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b197e970df26c5d48ccaf18603df107f0f3785db
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "33070722"
---
# <a name="lesson-1-2---setting-tool-options-and-layout"></a>Lección 1-2: Establecer las opciones de herramienta y el diseño
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Puede definir opciones que permiten configurar lo que mostrará la interfaz gráfica de usuario (GUI) del Asistente para la optimización de motor de base de datos al iniciarse, las fuentes utilizadas y otras funciones para facilitar el uso. Las prácticas de esta página le permitirán familiarizarse con las opciones que puede configurar y el modo de hacerlo.  
  
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
  
  
  
