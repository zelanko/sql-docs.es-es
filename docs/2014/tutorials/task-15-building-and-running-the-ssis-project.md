---
title: 'Tarea 15: Compilar y ejecutar el proyecto de SSIS | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 13adf4e0-216a-4992-b13d-b7b1e1629e77
ms.openlocfilehash: 1dc31f9b3df500e862236d4125fb1de99bc93eda
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63191855"
---
# <a name="task-15-building-and-running-the-ssis-project"></a>Tarea 15: Compilación y ejecución del proyecto de SSIS
  En esta tarea, compilará y ejecutará el proyecto de SSIS. Si tiene la versión de 64 bits de Excel 2010 instalado en el equipo, debe establecer el valor de **Run64BitRuntime** a **False** para el origen de Excel para que funcione.  
  
1.  En el **el Explorador de soluciones** ventana, haga clic en **proyecto** en el menú y haga clic en **propiedades de CleanseAndCurateSuppliers**.  
  
2.  En el **propiedades** cuadro de diálogo, expanda **propiedades de configuración** a izquierda y haga clic en **depuración**.  
  
3.  Establecer **Run64BitRuntime** a **False**.  
  
     ![Propiedades del proyecto CleanseAndCurateSuppliers](../../2014/tutorials/media/et-buildingandrunningthessisproject-01.jpg "las propiedades del proyecto CleanseAndCurateSuppliers")  
  
4.  Haga clic en **Aceptar** para cerrar el **propiedades** cuadro de diálogo.  
  
5.  Haga clic en **compilar** en la barra de menús y haga clic en **compilar CleanseAndCurateSuppliers**. Asegúrese de que no hay errores de compilación.  
  
6.  Haga clic en **depurar** en la barra de menú y haga clic en **Iniciar depuración**.  
  
7.  Revise los mensajes de la **progreso** ventana y compruebe que ha ejecutado y completado correctamente el paquete.  
  
     ![Resultado de la ventana de progreso](../../2014/tutorials/media/et-buildingandrunningthessisproject-02.jpg "da como resultado de la ventana de progreso")  
  
     ![Estado final de la ventana de progreso](../../2014/tutorials/media/et-buildingandrunningthessisproject-03.jpg "estado Final de la ventana de progreso")  
  
8.  Haga clic en **depurar** en la barra de menús y haga clic en **Detener depuración** para detener la sesión de depuración. Si se produce un error en el paquete, debe habilitar los visores de datos y ver cómo fluyen los datos entre los componentes.  
  
## <a name="next-step"></a>Paso siguiente  
 [Tarea 16: Comprobar con Master Data Manager](../../2014/tutorials/task-16-verifying-with-master-data-manager.md)  
  
  
