---
title: 'Tarea 8: Agregar condicional divide la transformación para dividir la salida de limpieza | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: d4ebe420-a4a9-4076-89d3-41abe726fc5c
caps.latest.revision: 6
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 40d01901ff90c22d4286e59c5d0589b07ad424a2
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37246135"
---
# <a name="task-8-adding-conditional-split-transform-to-split-cleansing-output"></a>Tarea 8: agregar la transformación División condicional para dividir el resultado de la limpieza
  En esta tarea, agregará una transformación División condicional al flujo de datos. La transformación División condicional puede dirigir filas a salidas diferentes en función del contenido de los datos. Para este tutorial, usará el **estado de registro** columna de salida de la transformación limpieza de DQS. En este tutorial solo cargará los registros correctos o corregidos en el servidor MDS. Por lo tanto, compruebe si el **estado de registro** es **correcto** o **corregido**y combinar los registros antes de cargar los registros a MDS.  
  
1.  Arrastrar y colocar **transformación División condicional** desde **común** sección la **cuadro de herramientas de SSIS** a la **de flujo de datos** ficha en **Limpiar datos de proveedor**.  
  
2.  Haga clic en **división condicional**y haga clic en **cambiar el nombre**. Tipo **elegir registros correctos y corregidos** y presione **ENTRAR**.  
  
3.  Conectar **limpiar datos de proveedor** y **elegir registros correctos y corregidos** mediante el conector azul.  
  
     ![Proveedor de limpiar datos -> corrección de selección & corregida](../../2014/tutorials/media/et-addingcsttosplitcleansingoutput-01.jpg "limpiar proveedor datos -> corrección de selección & corregida")  
  
4.  Haga doble clic en **elegir registros correctos y corregidos** en el **de flujo de datos** ficha.  
  
5.  Cambiar el **nombre de salida predeterminado** en la parte inferior de la pantalla para **correcto**.  
  
6.  Expanda **columnas** en el **panel superior izquierdo**.  
  
     ![Editor de transformación División condicional](../../2014/tutorials/media/et-addingcsttosplitcleansingoutput-02.jpg "Editor de transformación División condicional")  
  
7.  Arrastrar y colocar **estado de registro** a la **condición** columna.  
  
8.  Tipo **== "Corregido"** junto a **[estado de registro]** para el **condición** columna.  
  
9. Haga clic en **caso 1** en el **columna de nombre de salida**y cambie el nombre a **corregido**.  
  
10. Haga clic en **Aceptar** para cerrar el **Editor de transformación División condicional** cuadro de diálogo.  
  
## <a name="next-step"></a>Paso siguiente  
 [Tarea 9: Agregar la transformación Unión de todo para combinar los registros correctos y corregidos](../../2014/tutorials/task-9-adding-union-all-transform-to-combine-correct-and-corrected-records.md)  
  
  
