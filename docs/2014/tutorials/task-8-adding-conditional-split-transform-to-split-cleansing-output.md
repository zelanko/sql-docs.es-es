---
title: 'Tarea 8: agregar la transformación división condicional para dividir la salida de limpieza | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: d4ebe420-a4a9-4076-89d3-41abe726fc5c
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 57e8738edf77dae56454baba9ffc1b193146b110
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85006340"
---
# <a name="task-8-adding-conditional-split-transform-to-split-cleansing-output"></a>Tarea 8: Adición de la transformación División condicional para dividir el resultado de la limpieza
  En esta tarea, agregará una transformación División condicional al flujo de datos. La transformación División condicional puede dirigir filas a salidas diferentes en función del contenido de los datos. En este tutorial, usará la columna salida del **Estado de registro** de la transformación limpieza de DQS. En este tutorial solo cargará los registros correctos o corregidos en el servidor MDS. Por lo tanto, se comprueba si el **Estado del registro** es **correcto** o **corregido**, y se combinan los registros antes de cargar los registros en MDS.  
  
1.  Arrastre y coloque la **transformación división condicional** desde la sección **común** del **cuadro de herramientas de SSIS** hasta la pestaña flujo de **datos** en **limpiar datos del proveedor**.  
  
2.  Haga clic con el botón secundario en **división condicional**y haga clic en **cambiar nombre**. Escriba **elegir registros correctos y corregidos** y presione **entrar**.  
  
3.  Conecte **limpiar datos de proveedor** y **Seleccione los registros correctos y corregidos** con el conector azul.  
  
     ![Limpiar datos de proveedor: > seleccionar correcto & corregido](../../2014/tutorials/media/et-addingcsttosplitcleansingoutput-01.jpg "Limpiar datos de proveedor -> Corrección de selección & Corregida")  
  
4.  Haga doble clic en **seleccionar registros correctos y corregidos** en la pestaña **flujo de datos** .  
  
5.  Cambie el **nombre de salida predeterminado** en la parte inferior de la pantalla para **corregirlo**.  
  
6.  Expanda **columnas** en el **panel superior izquierdo**.  
  
     ![División condicional, editor de transformación](../../2014/tutorials/media/et-addingcsttosplitcleansingoutput-02.jpg "División condicional, editor de transformación")  
  
7.  Arrastre y coloque el **Estado del registro** en la columna **condición** .  
  
8.  Escriba **= = "corregido"** junto a **[estado del registro]** para la columna **condición** .  
  
9. Haga clic en el **caso 1** en la **columna Nombre de salida**y cambie el nombre a **corregido**.  
  
10. Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Editor de transformación división condicional** .  
  
## <a name="next-step"></a>siguiente paso  
 [Tarea 9: Adición de la transformación Unión de todo para combinar los registros correctos y corregidos](../../2014/tutorials/task-9-adding-union-all-transform-to-combine-correct-and-corrected-records.md)  
  
  
