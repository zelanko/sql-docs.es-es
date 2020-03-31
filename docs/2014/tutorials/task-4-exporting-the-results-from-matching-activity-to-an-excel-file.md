---
title: 'Tarea 4: Exportación de los resultados de la actividad de coincidencia a un archivo de Excel Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 644454c4-3c5a-469a-90ec-e51dc7fb99fc
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 4ed1d29af328a162eafadb1ce7a160c262bdcba3
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/28/2020
ms.locfileid: "78177253"
---
# <a name="task-4-exporting-the-results-from-matching-activity-to-an-excel-file"></a>Tarea 4: exportar los resultados de la actividad de coincidencia a un archivo de Excel
  En esta tarea, exportará los resultados de la actividad de coincidencia a un archivo de Excel.

1.  En la página **Exportar,** seleccione **Archivo de Excel** para tipo de **destino**.

2.  Seleccione la opción **Resultados de supervivencia.** En el proceso de supervivencia, DQS determina un registro de superviviente para cada clúster en función de la regla de **supervivencia** que seleccionó.

3.  Haga clic en **Examinar** y vaya a la carpeta donde desea almacenar el archivo de salida.

4.  Escriba **Cleansed and Matched Suppliers.xls** para el nombre y haga clic en **Abrir**.

5.  Confirme que **Registro dinámico** está seleccionado para la Regla **de supervivencia**. Al seleccionar esta opción, se elige el registro dinámico de cada clúster para la salida de un clúster. Las demás opciones de la regla de supervivencia son las siguientes:

    1.  **Registro más completo:** El registro de superviviente es el que tiene el mayor número de campos poblados.

    2.  **Registro más largo:** El registro de superviviente es el que tiene el mayor número de términos en los campos de origen.

    3.  **Registro más completo y más largo:** El registro de supervivientees es el que tiene el mayor número de campos poblados y tiene el mayor número de términos en cada campo.

     ![Exportar resultados de la página de coincidencias](../../2014/tutorials/media/et-exportingtheresultsfrommatoanexcelfile.jpg "Exportar resultados de la página de coincidencias")

6.  Haga clic en **Exportar** para exportar los resultados a un archivo de Excel.

7.  Haga clic en **Cerrar** para cerrar el cuadro de diálogo **Exportación coincidente.**

8.  Haga clic en **Finalizar** para finalizar la actividad coincidente.

9. Abra el archivo **Cleansed and Matched Suppliers.xlsx** y confirme que no ve ningún duplicado (SupplierID).

 Ahora, tiene datos de proveedor que se han limpiado y en el que se han buscado coincidencias para quitar valores duplicados.

## <a name="next-step"></a>siguiente paso
 [Lección 4: Almacenar datos de proveedor en MDS](../../2014/tutorials/lesson-4-storing-supplier-data-in-mds.md)


