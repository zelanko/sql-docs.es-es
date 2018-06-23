---
title: 'Tarea 11: Agregar condicional divide la transformación para filtrar duplicados | Documentos de Microsoft'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3094bd57-5cf4-4860-bf51-fadd1b309f94
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 7f61fa706659a6f71b2c69f18bcf7b694993ed00
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36113489"
---
# <a name="task-11-adding-conditional-split-transform-to-filter-duplicates"></a>Tarea 11: agregar la transformación División condicional para filtrar duplicados
  En esta tarea, agregará la transformación División condicional al flujo de datos. Esta transformación ayuda a filtrar duplicados del conjunto de registros de entrada. La transformación Agrupación aproximada agrupa los registros que son coincidentes y elige uno de ellos como registro dinámico. Todos los registros de un grupo tienen el mismo valor _key_out. El registro dinámica del grupo tiene el mismo valor de _key_in que de _key_out. Los demás registros del grupo tienen valores diferentes para _key_in y _key_out. Por tanto, cuando se filtra mediante la condición _key_in==_key_out, solo se obtiene la fila dinámica del grupo.  
  
1.  Arrastrar y colocar **división condicional** transformar de **común** sección la **cuadro de herramientas de SSIS** a la **de flujo de datos** ficha.  
  
2.  Haga clic en **transformación División condicional** en el **de flujo de datos** ficha y haga clic en **cambiar el nombre de**. Tipo de **filtrar duplicados** y presione **ENTRAR**.  
  
3.  Conectar **agrupar proveedores con Id. coincidentes** a **filtrar duplicados**.  
  
4.  Haga doble clic en **filtrar duplicados** para iniciar el **Editor de transformación División condicional** cuadro de diálogo.  
  
5.  Expanda **columnas** en el panel superior izquierdo.  
  
6.  Arrastrar y colocar **_key_in** a la **condición** columna.  
  
7.  Tipo == (igual que) junto a **_key_in** y arrastre y coloque **_key_out**.  
  
8.  Haga clic en **caso 1** en el **nombre de salida** columna, escriba **registros únicos**y presione **ENTRAR**.  
  
     ![Editor de transformación División condicional](../../2014/tutorials/media/et-addingconditionalsplittransformtofilterduplicates.jpg "Editor de transformación División condicional")  
  
9. Haga clic en **Aceptar** para cerrar el **Editor de transformación División condicional** cuadro de diálogo.  
  
## <a name="next-step"></a>Paso siguiente  
 [Tarea 12: Agregar transformación columna derivada para agregar las columnas necesarias en MDS](../../2014/tutorials/task-12-adding-derived-column-transform-to-add-columns-required-by-mds.md)  
  
  