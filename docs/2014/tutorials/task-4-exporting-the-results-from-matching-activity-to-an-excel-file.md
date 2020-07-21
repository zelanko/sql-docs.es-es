---
title: 'Tarea 4: exportar los resultados de la actividad de coincidencia a un archivo de Excel | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 644454c4-3c5a-469a-90ec-e51dc7fb99fc
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: fd85a523804232deff14f2e1da5485229f943dd2
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "84999664"
---
# <a name="task-4-exporting-the-results-from-matching-activity-to-an-excel-file"></a>Tarea 4: Exportación de los resultados de la actividad de coincidencia a un archivo de Excel
  En esta tarea, exportará los resultados de la actividad de coincidencia a un archivo de Excel.

1.  En la página **exportar** , seleccione **archivo de Excel** para el **tipo de destino**.

2.  Seleccione la opción **resultados de permanencia** . En el proceso de permanencia, DQS determina un registro de permanencia para cada clúster en función de la **regla de permanencia** seleccionada.

3.  Haga clic en **examinar** y navegue hasta la carpeta en la que desea almacenar el archivo de salida.

4.  Escriba **limpiar y coincidir Suppliers.xls** para el nombre y haga clic en **abrir**.

5.  Confirme que se ha seleccionado **registro dinámico** para la **regla de permanencia**. Al seleccionar esta opción, se elige el registro dinámico de cada clúster para la salida de un clúster. Las demás opciones de la regla de supervivencia son las siguientes:

    1.  **Registro más completo:** El registro de permanencia es el que tiene el mayor número de campos rellenos.

    2.  **Registro más largo:** El registro de permanencia es el que tiene el mayor número de términos en los campos de origen.

    3.  **Registro más completo y más largo:** El registro de permanencia es el que tiene el mayor número de campos rellenos y tiene el mayor número de términos en cada campo.

     ![Exportar resultados de la página de coincidencias](../../2014/tutorials/media/et-exportingtheresultsfrommatoanexcelfile.jpg "Exportar resultados de la página de coincidencias")

6.  Haga clic en **exportar** para exportar los resultados a un archivo de Excel.

7.  Haga clic en **cerrar** para cerrar el cuadro de diálogo **exportar correspondiente** .

8.  Haga clic en **Finalizar** para finalizar la actividad de búsqueda de coincidencias.

9. Abra el archivo **limpio y el Suppliers.xlsxde coincidencia** y confirme que no ve ningún duplicado (IdProveedor).

 Ahora, tiene datos de proveedor que se han limpiado y en el que se han buscado coincidencias para quitar valores duplicados.

## <a name="next-step"></a>siguiente paso
 [Lección 4: Almacenamiento de datos de proveedor en MDS](../../2014/tutorials/lesson-4-storing-supplier-data-in-mds.md)


