---
title: 'Tarea 8: Agregar condicional divide la transformación para dividir la salida de limpieza | Documentos de Microsoft'
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
ms.topic: article
ms.assetid: d4ebe420-a4a9-4076-89d3-41abe726fc5c
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 6dc3b98e03a7940841bc97012c1a4e4220bb970d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36196852"
---
# <a name="task-8-adding-conditional-split-transform-to-split-cleansing-output"></a>Tarea 8: agregar la transformación División condicional para dividir el resultado de la limpieza
  En esta tarea, agregará una transformación División condicional al flujo de datos. La transformación División condicional puede dirigir filas a salidas diferentes en función del contenido de los datos. Para este tutorial, use la **estado de registro** columna de salida de la transformación limpieza de DQS. En este tutorial solo cargará los registros correctos o corregidos en el servidor MDS. Por tanto, compruebe si el **estado de registro** es **correcto** o **corregido**y combinar los registros antes de cargarlos en MDS.  
  
1.  Arrastrar y colocar **transformación División condicional** de **común** sección el **cuadro de herramientas de SSIS** a la **de flujo de datos** pestaña **Limpiar datos de proveedor**.  
  
2.  Haga clic en **división condicional**y haga clic en **cambiar el nombre de**. Tipo de **elegir registros correctos y corregidos** y presione **ENTRAR**.  
  
3.  Conectar **limpiar datos de proveedor** y **elegir registros correctos y corregidos** mediante el conector azul.  
  
     ![Proveedor de limpiar datos -> corrección de selección & corregida](../../2014/tutorials/media/et-addingcsttosplitcleansingoutput-01.jpg "limpiar proveedor datos -> corrección de selección & corregida")  
  
4.  Haga doble clic en **elegir registros correctos y corregidos** en el **de flujo de datos** ficha.  
  
5.  Cambiar el **nombre de salida predeterminado** en la parte inferior de la pantalla para **correcto**.  
  
6.  Expanda **columnas** en el **panel superior izquierdo**.  
  
     ![Editor de transformación División condicional](../../2014/tutorials/media/et-addingcsttosplitcleansingoutput-02.jpg "Editor de transformación División condicional")  
  
7.  Arrastrar y colocar **estado de registro** a la **condición** columna.  
  
8.  Tipo de **== "Corregido"** junto a **[estado de registro]** para el **condición** columna.  
  
9. Haga clic en **caso 1** en el **columna de nombre de salida**y cambie el nombre a **corregido**.  
  
10. Haga clic en **Aceptar** para cerrar el **Editor de transformación División condicional** cuadro de diálogo.  
  
## <a name="next-step"></a>Paso siguiente  
 [Tarea 9: Agregar la unión transformación todo para combinar registros correctos y corregidos](../../2014/tutorials/task-9-adding-union-all-transform-to-combine-correct-and-corrected-records.md)  
  
  