---
title: 'Tarea 7: agregar la transformación limpieza de DQS al flujo de datos | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 0b749c71-dfb6-493a-804f-600290d46eef
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 0978452104eb9a55d49dfa9f851ef7578489db26
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85006479"
---
# <a name="task-7-adding-dqs-cleansing-transform-to-the-data-flow"></a>Tarea 7: Adición de la transformación Limpieza de DQS al flujo de datos
  En esta tarea, agregará la transformación Limpieza de DQS al flujo de datos para limpiar los datos de proveedor de entrada mediante DQS. Vea **[transformación limpieza de DQS](https://msdn.microsoft.com/library/ee677619.aspx)** para obtener más detalles sobre la transformación.  
  
1.  Haga clic con el botón secundario en **limpieza de DQS** en la pestaña **flujo de datos** y haga clic en **cambiar nombre**. Escriba **limpiar datos de proveedor**y presione **entrar**.  
  
2.  Seleccione **leer datos de proveedor del archivo de Excel**; Arrastre el conector azul para **limpiar los datos de proveedor**. Los componentes ahora están conectados.  
  
     ![Leer datos de proveedor: > limpiar los datos de proveedor](../../2014/tutorials/media/et-addingdqscleansingtransformtothedataflow-01.jpg "Leer datos de proveedor -> Limpiar datos de proveedor")  
  
3.  Haga doble clic en **limpiar datos de proveedor**.  
  
4.  En el **Editor de transformación limpieza de DQS**, haga clic en **nuevo** junto a la lista desplegable **Administrador de conexiones de calidad de datos**.  
  
5.  En el cuadro de diálogo **Administrador de conexiones de limpieza de DQS** , escriba **(local)** o **punto** (.) para conectarse al servidor local. En esta lección se da por supuesto que ha instalado DQS en un servidor local.  
  
6.  Haga clic en **probar conexión** para probar la conexión con el servidor DQS.  
  
7.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo.  
  
8.  Seleccione **proveedores** en la **base de conocimiento de calidad de datos**.  
  
     ![Editor de transformación Limpieza de DQS - Knowledge Base de los proveedores](../../2014/tutorials/media/et-addingdqscleansingtransformtothedataflow-02.jpg "Editor de transformación Limpieza de DQS - Knowledge Base de los proveedores")  
  
9. Cambie a la pestaña **asignación** en la parte superior.  
  
10. En **columnas de entrada disponibles**, **Seleccione Nombre del proveedor**, **ContactEmailAddress**, línea de **Dirección**, **ciudad**, **Estado**, **país**y **código postal** . para ello, active las casillas de verificación.  
  
     ![Editor de transformación Limpieza de DQS - Asignaciones](../../2014/tutorials/media/et-addingdqscleansingtransformtothedataflow-03.jpg "Editor de transformación Limpieza de DQS - Asignaciones")  
  
11. En el panel inferior, asigne estas columnas mediante listas desplegables de la columna **dominio** :  
  
    |Columna|Dominio|  
    |------------|------------|  
    |Nombre del proveedor|Nombre del proveedor|  
    |ContactEmailAddress|Dirección de correo electrónico de contacto|  
    |Address Line|Address Line|  
    |City|City|  
    |State|State|  
    |País|País|  
    |Zip Code|Zip|  
  
12. Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Editor de transformación limpieza de DQS** .  
  
## <a name="next-step"></a>siguiente paso  
 [Tarea 8: Adición de la transformación División condicional para dividir el resultado de la limpieza](../../2014/tutorials/task-8-adding-conditional-split-transform-to-split-cleansing-output.md)  
  
  
