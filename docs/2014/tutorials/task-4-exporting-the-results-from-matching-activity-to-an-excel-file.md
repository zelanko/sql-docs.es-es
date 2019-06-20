---
title: 'Tarea 4: Exportar los resultados de la actividad de coincidencia a un archivo de Excel | Microsoft Docs'
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
ms.openlocfilehash: 74164c6f6178acbcfe4784dac855c7c0485fc3b0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65489443"
---
# <a name="task-4-exporting-the-results-from-matching-activity-to-an-excel-file"></a>Tarea 4: Exportación de los resultados de la actividad de coincidencia a un archivo de Excel
  En esta tarea, exportará los resultados de la actividad de coincidencia a un archivo de Excel.  
  
1.  En el **exportar** página, seleccione **archivo de Excel** para el **tipo de destino**.  
  
2.  Seleccione **los resultados de permanencia** opción. En el proceso de permanencia, DQS determina un registro de permanencia para cada clúster según la **regla de permanencia** que ha seleccionado.  
  
3.  Haga clic en **examinar** y navegue hasta la carpeta donde desea almacenar el archivo de salida.  
  
4.  Tipo **Cleansed and Matched Suppliers.xls** para el nombre y haga clic en **abierto**.  
  
5.  Confirme que **registro dinámico** está seleccionada para la **regla de permanencia**. Al seleccionar esta opción, se elige el registro dinámico de cada clúster para la salida de un clúster. Las demás opciones de la regla de supervivencia son las siguientes:  
  
    1.  **Registro más completo:** El registro de permanencia es el que tiene el mayor número de campos rellenos.  
  
    2.  **Registro más largo:** El registro de permanencia es el que tiene el mayor número de términos en campos de origen.  
  
    3.  **Registro más completo y más largo:** El registro de permanencia es el que tiene el mayor número de campos rellenos y con el mayor número de términos en cada campo.  
  
     ![Exportar los resultados de la página coincidencia](../../2014/tutorials/media/et-exportingtheresultsfrommatoanexcelfile.jpg "exportar los resultados de la página coincidencia")  
  
6.  Haga clic en **exportar** para exportar los resultados a un archivo de Excel.  
  
7.  Haga clic en **cerrar** para cerrar el **exportación de coincidencia** cuadro de diálogo.  
  
8.  Haga clic en **finalizar** para finalizar la actividad de coincidencia.  
  
9. Abra el **Cleansed and Matched Suppliers.xlsx** de archivo y confirme que no ve ningún duplicado (SupplierID).  
  
 Ahora, tiene datos de proveedor que se han limpiado y en el que se han buscado coincidencias para quitar valores duplicados.  
  
## <a name="next-step"></a>Paso siguiente  
 [Lección 4: Almacenar datos de proveedor en MDS](../../2014/tutorials/lesson-4-storing-supplier-data-in-mds.md)  
  
  
