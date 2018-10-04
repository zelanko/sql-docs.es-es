---
title: Establecer opciones de herramienta y el diseño | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- Database Engine [SQL Server], tutorials
ms.assetid: 43e97ce0-97bc-4a27-9485-5bbeb7190b85
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 023a38a1d3b5c09fc7e1447ecd026d133abca1db
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48166507"
---
# <a name="setting-tool-options-and-layout"></a>Configurar las opciones de herramienta y el diseño
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
 [Lección 2: Usar el Asistente para la optimización de motor de base de datos](../../relational-databases/performance/database-engine-tuning-advisor.md)  
  
  
