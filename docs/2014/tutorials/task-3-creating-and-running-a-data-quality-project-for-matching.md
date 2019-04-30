---
title: 'Tarea 3: Crear y ejecutar un proyecto de calidad de datos para buscar coincidencias | Microsoft Docs'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 6260e911-ea8b-4c69-a39d-d1bccd565a32
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: abca2dcf68472884eb3c1e42f0ff9c14004098c5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63250022"
---
# <a name="task-3-creating-and-running-a-data-quality-project-for-matching"></a>Tarea 3: Creación y ejecución de un proyecto de calidad de datos para buscar coincidencias
  En esta tarea, creará un proyecto de calidad de datos para la actividad de búsqueda de coincidencias y ejecutará el proceso de coincidencia en los datos limpios de proveedores para quitar duplicados en los datos.  
  
1.  En la página principal de **cliente DQS**, haga clic en **nuevo proyecto de calidad de datos**.  
  
2.  Tipo **quitar proveedores duplicados** desde el **nombre del proyecto**.  
  
3.  Seleccione **proveedores** en la lista de artículos de KB para la **usar Base de conocimiento** campo. En la lección anterior creó una directiva de coincidencia en esta base de conocimiento.  
  
4.  Seleccione **coincidencia** desde el **lista de actividades** desde el panel de la esquina inferior derecha.  
  
     ![Nuevo proyecto de calidad de datos - coincidencia seleccionada](../../2014/tutorials/media/et-creatingandrunningadqpformatching.jpg "nuevo proyecto de calidad de datos - coincidencia seleccionada")  
  
5.  Haga clic en **Siguiente**.  
  
6.  En la página **Asignación** , seleccione **Archivo de Excel** en **Origen de datos**.  
  
7.  Haga clic en **examinar** y seleccione **Cleansed Supplier List.xls**, que es el archivo de salida de la actividad de limpieza.  
  
8.  Mapa **SupplierID** columna de origen a la **Id. de proveedor** dominio, **Supplier Name** columna **Supplier Name** dominio y **ContactEmailAddress** columna **correo electrónico de contacto** dominio.  
  
9. Haga clic en **siguiente** para cambiar a la **coincidencia** página.  
  
10. Haga clic en **iniciar** para iniciar el proceso de coincidencia. Debe ver unos resultados similares a los de la tarea anterior porque ha usado el mismo archivo de entrada para definir la directiva de coincidencia.  
  
11. Examine todos los registros coincidentes y su puntuación de coincidencia en el cuadro de lista. Los resultados deben ser los mismos que los de la tarea anterior. Vea los pasos de la tarea anterior para analizar los resultados de esta actividad de coincidencia.  
  
12. Haga clic en **siguiente** para cambiar a la **exportar** página.  
  
## <a name="next-step"></a>Paso siguiente  
 [Tarea 4: Exportar los resultados de la actividad de coincidencia a un archivo de Excel](../../2014/tutorials/task-4-exporting-the-results-from-matching-activity-to-an-excel-file.md)  
  
  
