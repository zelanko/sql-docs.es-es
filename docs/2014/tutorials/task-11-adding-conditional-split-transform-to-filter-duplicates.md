---
title: 'Tarea 11: agregar la transformación división condicional para filtrar duplicados | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 3094bd57-5cf4-4860-bf51-fadd1b309f94
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 71b050e49440764d355d4658607600c135741f50
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "65476750"
---
# <a name="task-11-adding-conditional-split-transform-to-filter-duplicates"></a>Tarea 11: Adición de la transformación División condicional para filtrar duplicados
  En esta tarea, agregará la transformación División condicional al flujo de datos. Esta transformación ayuda a filtrar duplicados del conjunto de registros de entrada. La transformación Agrupación aproximada agrupa los registros que son coincidentes y elige uno de ellos como registro dinámico. Todos los registros de un grupo tienen el mismo valor _key_out. El registro dinámica del grupo tiene el mismo valor de _key_in que de _key_out. Los demás registros del grupo tienen valores diferentes para _key_in y _key_out. Por tanto, cuando se filtra mediante la condición _key_in==_key_out, solo se obtiene la fila dinámica del grupo.  
  
1.  Arrastre y coloque la transformación **división condicional** desde la sección **común** del **cuadro de herramientas de SSIS** hasta la pestaña flujo de **datos** .  
  
2.  Haga clic con el botón secundario en **transformación división condicional** en la pestaña **flujo de datos** y haga clic en **cambiar nombre**. Escriba **filtrar duplicados** y presione **entrar**.  
  
3.  Conectar **proveedores de grupos con identificadores coincidentes** para **filtrar duplicados**.  
  
4.  Haga doble clic en **filtrar duplicados** para iniciar el cuadro de diálogo **Editor de transformación división condicional** .  
  
5.  Expanda **columnas** en el panel superior izquierdo.  
  
6.  Arrastre y coloque **_key_in** a la columna **condición** .  
  
7.  Type = = (es igual a) junto a **_key_in** y arrastrar y colocar **_key_out**.  
  
8.  Haga clic en el **caso 1** en la columna **nombre de salida** , escriba **Registros únicos**y presione **entrar**.  
  
     ![División condicional, editor de transformación](../../2014/tutorials/media/et-addingconditionalsplittransformtofilterduplicates.jpg "División condicional, editor de transformación")  
  
9. Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Editor de transformación división condicional** .  
  
## <a name="next-step"></a>siguiente paso  
 [Tarea 12: Adición de la transformación Columna derivada para agregar las columnas necesarias en MDS](../../2014/tutorials/task-12-adding-derived-column-transform-to-add-columns-required-by-mds.md)  
  
  
