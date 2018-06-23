---
title: 'Tarea 7: Agregar transformación al flujo de datos de limpieza de DQS | Documentos de Microsoft'
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
ms.assetid: 0b749c71-dfb6-493a-804f-600290d46eef
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 10b0fb12ace5a113bbde03cecf803a37b49b1974
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36203541"
---
# <a name="task-7-adding-dqs-cleansing-transform-to-the-data-flow"></a>Tarea 7: agregar la transformación Limpieza de DQS al flujo de datos
  En esta tarea, agregará la transformación Limpieza de DQS al flujo de datos para limpiar los datos de proveedor de entrada mediante DQS. Vea **[transformación limpieza de DQS](http://msdn.microsoft.com/library/ee677619.aspx)** para obtener más información acerca de la transformación.  
  
1.  Haga clic en **limpieza de DQS** en el **de flujo de datos** ficha y haga clic en **cambiar el nombre de**. Tipo de **limpiar datos de proveedor**y presione **ENTRAR**.  
  
2.  Seleccione **datos de proveedor de lectura de archivo de Excel**; arrastre el conector azul hasta **limpiar datos de proveedor**. Los componentes ahora están conectados.  
  
     ![Leer datos de proveedor -> Limpiar datos de proveedor](../../2014/tutorials/media/et-addingdqscleansingtransformtothedataflow-01.jpg "leer datos de proveedor -> Limpiar datos de proveedor")  
  
3.  Haga doble clic en **limpiar datos de proveedor**.  
  
4.  En el **Editor de transformación limpieza de DQS**, haga clic en **New** junto a la **lista desplegable de administrador de conexiones de calidad de datos**.  
  
5.  En el **Administrador de conexiones de limpieza de DQS** cuadro de diálogo, escriba **(local)** o **período** (.) para conectarse al servidor local. En esta lección se da por supuesto que ha instalado DQS en un servidor local.  
  
6.  Haga clic en **Probar conexión** para probar la conexión con el servidor DQS.  
  
7.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo.  
  
8.  Seleccione **proveedores** para el **Base de conocimiento de calidad de datos**.  
  
     ![Editor de transformación - proveedores KB limpieza de DQS](../../2014/tutorials/media/et-addingdqscleansingtransformtothedataflow-02.jpg "Editor de transformación - proveedores KB limpieza de DQS")  
  
9. Cambie a la **asignación** ficha en la parte superior.  
  
10. De **columnas de entrada disponibles**, seleccione **Supplier Name**, **ContactEmailAddress**, **Address Line**, **City**, **Estado**, **país**, y **código postal** seleccionando las casillas de verificación.  
  
     ![Editor de transformación - asignaciones de limpieza de DQS](../../2014/tutorials/media/et-addingdqscleansingtransformtothedataflow-03.jpg "Editor de transformación - asignaciones de limpieza de DQS")  
  
11. En el panel inferior, asigne estas columnas mediante listas desplegables en el **dominio** columna:  
  
    |columna|Dominio|  
    |------------|------------|  
    |Nombre de proveedor|Nombre de proveedor|  
    |ContactEmailAddress|Póngase en contacto con el correo electrónico|  
    |Address Line|Address Line|  
    |City|City|  
    |State|State|  
    |País|País|  
    |Zip Code|Zip|  
  
12. Haga clic en **Aceptar** para cerrar el **Editor de transformación limpieza de DQS** cuadro de diálogo.  
  
## <a name="next-step"></a>Paso siguiente  
 [Tarea 8: Agregar la transformación División condicional para dividir el resultado de limpieza](../../2014/tutorials/task-8-adding-conditional-split-transform-to-split-cleansing-output.md)  
  
  