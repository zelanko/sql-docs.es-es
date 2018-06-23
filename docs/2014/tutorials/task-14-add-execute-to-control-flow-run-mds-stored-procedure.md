---
title: 'Tarea 14: Agregar tarea Ejecutar SQL al flujo de Control para ejecutar el procedimiento almacenado de MDS | Documentos de Microsoft'
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
ms.assetid: 9a5d1b52-d505-4e6f-8a89-569329c094e2
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 3d364f3e0a2fbff167336bffa6ea5092d0954d14
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36106671"
---
# <a name="task-14-adding-execute-sql-task-to-control-flow-to-run-the-stored-procedure-for-mds"></a>Tarea 14: agregar la tarea Ejecutar SQL al flujo de control para ejecutar el procedimiento almacenado de MDS
  Después de cargar datos en las tablas de ensayo de MDS, hay que ejecutar un procedimiento almacenado asociado a esa tabla para cargar los datos de las tablas de ensayo en las tablas adecuadas de la base de datos de MDS. Este procedimiento almacenado tiene dos parámetros requeridos que tiene que pasar: LogFlag y VersionName. LogFlag especifica si las transacciones se registran durante el proceso de almacenamiento provisional y VersionName representa la versión del modelo. Vea [procedimiento almacenado provisionalmente](http://msdn.microsoft.com/library/hh231028.aspx) tema para obtener más detalles.  
  
 En esta tarea, agregará la tarea Ejecutar SQL al flujo de control para invocar el procedimiento almacenado con el fin de cargar los datos almacenados provisionalmente en las tablas adecuadas de MDS.  
  
1.  Ahora, cambie a la **flujo de Control** ficha.  
  
2.  Arrastrar y colocar **tarea Ejecutar SQL** desde el **cuadro de herramientas de SSIS** a la **flujo de Control** ficha.  
  
3.  Haga clic en **tarea Ejecutar SQL** en el **flujo de Control** ficha y haga clic en **cambiar el nombre de**. Tipo de **desencadenar procedimiento almacenado para cargar datos en MDS** y presione **ENTRAR**.  
  
4.  Conectar **recepción, limpieza, coincidencia y reparar datos de proveedor** a **desencadenar procedimiento almacenado para cargar datos** mediante el conector verde.  
  
     ![Conectarse a la tarea Ejecutar SQL](../../2014/tutorials/media/et-addingesqltasktocftorunthespformds-01.jpg "conectarse para la tarea Ejecutar SQL")  
  
5.  Mediante el **Variables** ventana, agregue dos variables nuevas con la configuración siguiente. Si no ve el **Variables** ventana, haga clic en **SSIS** en la barra de menús y haga clic en **Variables**.  
  
    |Nombre|Tipo de datos|Valor|  
    |----------|---------------|-----------|  
    |LogFlag|Int32|1|  
    |VersionName|String|VERSION_1|  
  
     ![Ventana de Variables SSIS](../../2014/tutorials/media/et-addingesqltasktocftorunthespformds-02.jpg "ventana de Variables SSIS")  
  
6.  Haga doble clic en **desencadenar procedimiento almacenado para cargar datos en MDS**.  
  
7.  En el **Editor de la tarea Ejecutar SQL** cuadro de diálogo, seleccione **(local). MDS** (o **localhost. MDS**) para **conexión**.  
  
8.  Tipo **EXEC [stg]. [ ¿udp_Supplier_Leaf]?,?,?** para **instrucción SQL**. Puede comprobar el nombre mediante SQL Server Management Studio.  
  
     ![Ejecutar la configuración General de cuadro de diálogo Editor de SQL -](../../2014/tutorials/media/et-addingesqltasktocftorunthespformds-03.jpg "ejecutar cuadro de diálogo Editor de SQL - configuración General")  
  
9. Haga clic en **asignación de parámetros** desde el menú de la izquierda.  
  
10. En el **asignación de parámetros** página, haga clic en **agregar** para agregar una asignación. Maximice la ventana y cambie el tamaño de las columnas de forma que pueda ver correctamente los valores de las listas desplegables.  
  
11. Seleccione **User:: VersionName** en la lista desplegable de la **nombre de Variable**.  
  
12. Seleccione **NVARCHAR** para **tipo de datos**.  
  
13. Tipo de **0** (cero) para **nombre de parámetro**.  
  
14. Repita los cuatro pasos anteriores para agregar dos variables más.  
  
    |Nombre de variable|Tipo de datos (importante)|Nombre de parámetro|  
    |-------------------|-----------------------------|--------------------|  
    |User::LogFlag|LONG|1|  
    |User::BatchTag|NVARCHAR|2|  
  
     ![Ejecutar el Editor de la tarea SQL - asignación de parámetros](../../2014/tutorials/media/et-addingesqltasktocftorunthespformds-04.jpg "ejecutar el Editor de la tarea SQL - asignación de parámetros")  
  
15. Haga clic en **Aceptar** para cerrar el **Editor ejecutar SQL** cuadro de diálogo.  
  
## <a name="next-step"></a>Paso siguiente  
 [Tarea 15: Compilar y ejecutar el proyecto SSIS](../../2014/tutorials/task-15-building-and-running-the-ssis-project.md)  
  
  