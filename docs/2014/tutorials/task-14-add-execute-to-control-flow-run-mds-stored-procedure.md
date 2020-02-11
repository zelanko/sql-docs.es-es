---
title: 'Tarea 14: agregar la tarea ejecutar SQL al flujo de control para ejecutar el procedimiento almacenado para MDS | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 9a5d1b52-d505-4e6f-8a89-569329c094e2
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 3fe1eb6032d9d550b36252e16eee51c98c5d2384
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "65477099"
---
# <a name="task-14-adding-execute-sql-task-to-control-flow-to-run-the-stored-procedure-for-mds"></a>Tarea 14: agregar la tarea Ejecutar SQL al flujo de control para ejecutar el procedimiento almacenado de MDS
  Después de cargar datos en las tablas de ensayo de MDS, hay que ejecutar un procedimiento almacenado asociado a esa tabla para cargar los datos de las tablas de ensayo en las tablas adecuadas de la base de datos de MDS. Este procedimiento almacenado tiene dos parámetros requeridos que tiene que pasar: LogFlag y VersionName. LogFlag especifica si las transacciones se registran durante el proceso de almacenamiento provisional y VersionName representa la versión del modelo. Vea el tema sobre [procedimientos almacenados preconfigurados](https://msdn.microsoft.com/library/hh231028.aspx) para obtener más detalles.  
  
 En esta tarea, agregará la tarea Ejecutar SQL al flujo de control para invocar el procedimiento almacenado con el fin de cargar los datos almacenados provisionalmente en las tablas adecuadas de MDS.  
  
1.  Ahora, cambie a la pestaña **flujo de control** .  
  
2.  Arrastre y coloque la **tarea ejecutar SQL** desde el **cuadro de herramientas de SSIS** hasta la pestaña flujo de **control** .  
  
3.  Haga clic con el botón secundario en **tarea ejecutar SQL** en la pestaña **flujo de control** y haga clic en **cambiar nombre**. Escriba **desencadenar procedimiento almacenado para cargar datos en MDS** y presione **entrar**.  
  
4.  Conecte **Receive, cleane, Match y ajustar Supplier Data** para **desencadenar el procedimiento almacenado para cargar datos** mediante el conector verde.  
  
     ![Conexión a tarea Ejecutar SQL](../../2014/tutorials/media/et-addingesqltasktocftorunthespformds-01.jpg "Conexión a tarea Ejecutar SQL")  
  
5.  Mediante la ventana **variables** , agregue dos nuevas variables con la siguiente configuración. Si no ve la ventana **variables** , haga clic en **SSIS** en la barra de menús y, a continuación, haga clic en **variables**.  
  
    |Nombre|Tipo de datos|Value|  
    |----------|---------------|-----------|  
    |LogFlag|Int32|1|  
    |VersionName|String|VERSION_1|  
  
     ![Ventana Variables de SSIS](../../2014/tutorials/media/et-addingesqltasktocftorunthespformds-02.jpg "Ventana Variables de SSIS")  
  
6.  Haga doble clic en **procedimiento almacenado de desencadenador para cargar datos en MDS**.  
  
7.  En el cuadro de diálogo Editor de la **tarea ejecutar SQL** , seleccione **(local). MDS** (o **localhost). MDS**) para la **conexión**.  
  
8.  Escriba **exec [STG]. [ udp_Supplier_Leaf]?,?,?** **instrucción SQL**. Puede comprobar el nombre mediante SQL Server Management Studio.  
  
     ![Cuadro de diálogo Editor de la tarea Ejecutar SQL - Configuración general](../../2014/tutorials/media/et-addingesqltasktocftorunthespformds-03.jpg "Cuadro de diálogo Editor de la tarea Ejecutar SQL - Configuración general")  
  
9. Haga clic en **asignación de parámetros** en el menú de la izquierda.  
  
10. En la página **asignación de parámetros** , haga clic en **Agregar** para agregar una asignación. Maximice la ventana y cambie el tamaño de las columnas de forma que pueda ver correctamente los valores de las listas desplegables.  
  
11. Seleccione **User:: VersionName** en la lista desplegable del nombre de la **variable**.  
  
12. Seleccione **nvarchar** en **tipo de datos**.  
  
13. Escriba **0** (cero) para **el nombre del parámetro**.  
  
14. Repita los cuatro pasos anteriores para agregar dos variables más.  
  
    |Nombre de la variable|Tipo de datos (importante)|Nombre de parámetro|  
    |-------------------|-----------------------------|--------------------|  
    |User::LogFlag|LONG|1|  
    |User::BatchTag|NVARCHAR|2|  
  
     ![Editor de la tarea Ejecutar SQL - Asignación de parámetros](../../2014/tutorials/media/et-addingesqltasktocftorunthespformds-04.jpg "Editor de la tarea Ejecutar SQL - Asignación de parámetros")  
  
15. Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Editor de ejecutar SQL** .  
  
## <a name="next-step"></a>siguiente paso  
 [Tarea 15: compilar y ejecutar el proyecto de SSIS](../../2014/tutorials/task-15-building-and-running-the-ssis-project.md)  
  
  
