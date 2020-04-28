---
title: 'Tarea 3: crear y ejecutar un proyecto de calidad de datos para buscar coincidencias | Microsoft Docs'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 6260e911-ea8b-4c69-a39d-d1bccd565a32
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: c6953214bd5e5353643cb16b75ed51ac18783256
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "78171774"
---
# <a name="task-3-creating-and-running-a-data-quality-project-for-matching"></a>Tarea 3: Creación y ejecución de un proyecto de calidad de datos para buscar coincidencias
  En esta tarea, creará un proyecto de calidad de datos para la actividad de búsqueda de coincidencias y ejecutará el proceso de coincidencia en los datos limpios de proveedores para quitar duplicados en los datos.

1.  En la Página principal del **cliente DQS**, haga clic en **nuevo proyecto de calidad de datos**.

2.  Escriba **quitar proveedores duplicados** del **nombre del proyecto**.

3.  Seleccione **proveedores** en la lista de KB del campo **usar base de conocimiento** . En la lección anterior creó una directiva de coincidencia en esta base de conocimiento.

4.  Seleccione **coincidencia** en la **lista de actividades** en el panel de la parte inferior derecha.

     ![Nuevo proyecto de calidad de datos - Coincidencia seleccionada](../../2014/tutorials/media/et-creatingandrunningadqpformatching.jpg "Nuevo proyecto de calidad de datos - Coincidencia seleccionada")

5.  Haga clic en **Next**.

6.  En la página **Asignación** , seleccione **Archivo de Excel** en **Origen de datos**.

7.  Haga clic en **examinar** y seleccione **cleaned Supplier List. xls**, que es el archivo de salida de la actividad de limpieza.

8.  Asigne la columna de origen **SupplierID** al dominio ID. de **proveedor** , la columna **nombre de proveedor** a dominio nombre de **proveedor** y la columna **ContactEmailAddress** al dominio **correo electrónico de contacto** .

9. Haga clic en **siguiente** para cambiar a la página de **búsqueda de coincidencias** .

10. Haga clic en **iniciar** para iniciar el proceso de búsqueda de coincidencias. Debe ver unos resultados similares a los de la tarea anterior porque ha usado el mismo archivo de entrada para definir la directiva de coincidencia.

11. Examine todos los registros coincidentes y su puntuación de coincidencia en el cuadro de lista. Los resultados deben ser los mismos que los de la tarea anterior. Vea los pasos de la tarea anterior para analizar los resultados de esta actividad de coincidencia.

12. Haga clic en **siguiente** para cambiar a la página **exportar** .

## <a name="next-step"></a>siguiente paso
 [Tarea 4: Exportación de los resultados de la actividad de coincidencia a un archivo de Excel](../../2014/tutorials/task-4-exporting-the-results-from-matching-activity-to-an-excel-file.md)


