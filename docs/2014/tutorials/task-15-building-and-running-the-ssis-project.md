---
title: 'Tarea 15: compilar y ejecutar el proyecto de SSIS | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 13adf4e0-216a-4992-b13d-b7b1e1629e77
ms.author: lle
author: lrtoyou1223
ms.openlocfilehash: 50b313f63ae434a96d6c0e38f3c8b600914c806d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66822993"
---
# <a name="task-15-building-and-running-the-ssis-project"></a>Tarea 15: compilar y ejecutar el proyecto de SSIS

  En esta tarea, compilará y ejecutará el proyecto de SSIS. Si tiene instalada la versión de 64 bits de Excel 2010 en el equipo, debe establecer el valor de **Run64BitRuntime** en **false** para que el origen de Excel funcione.  
  
1.  En la ventana de **Explorador de soluciones** , haga clic en **proyecto** en el menú y, a continuación, haga clic en **propiedades de CleanseAndCurateSuppliers**.  
  
2.  En el cuadro de diálogo **propiedades** , expanda **propiedades de configuración** a la izquierda y haga clic en **depuración**.  
  
3.  Establezca **Run64BitRuntime** en **false**.  
  
     ![Propiedades del proyecto CleanseAndCurateSuppliers](../../2014/tutorials/media/et-buildingandrunningthessisproject-01.jpg "Propiedades del proyecto CleanseAndCurateSuppliers")  
  
4.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo **propiedades** .  
  
5.  Haga clic en **compilar** en la barra de menús y haga clic en **generar CleanseAndCurateSuppliers**. Asegúrese de que no hay errores de compilación.  
  
6.  Haga clic en **depurar** en la barra de menús y haga clic en **iniciar depuración**.  
  
7.  Revise los mensajes en la ventana de **progreso** y compruebe que el paquete se ejecutó y finalizó correctamente.  
  
     ![Resultados de la ventana de progreso](../../2014/tutorials/media/et-buildingandrunningthessisproject-02.jpg "Resultados de la ventana de progreso")  
  
     ![Estado final de la ventana de progreso](../../2014/tutorials/media/et-buildingandrunningthessisproject-03.jpg "Estado final de la ventana de progreso")  
  
8.  Haga clic en **depurar** en la barra de menús y en **detener depuración** para detener la sesión de depuración. Si se produce un error en el paquete, debe habilitar los visores de datos y ver cómo fluyen los datos entre los componentes.  
  
## <a name="next-step"></a>siguiente paso  
 [Tarea 16: comprobar con Master Data Manager](../../2014/tutorials/task-16-verifying-with-master-data-manager.md)  
  
  
