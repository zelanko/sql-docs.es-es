---
title: 'Tarea 4: Exportar los resultados de la actividad de coincidencia a un archivo de Excel | Microsoft Docs'
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
ms.topic: conceptual
ms.assetid: 644454c4-3c5a-469a-90ec-e51dc7fb99fc
caps.latest.revision: 6
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 13fcd1b697be6ad7aeebd933da1059955dc0649f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37179004"
---
# <a name="task-4-exporting-the-results-from-matching-activity-to-an-excel-file"></a>Tarea 4: exportar los resultados de la actividad de coincidencia a un archivo de Excel
  En esta tarea, exportará los resultados de la actividad de coincidencia a un archivo de Excel.  
  
1.  En el **exportar** página, seleccione **archivo de Excel** para el **tipo de destino**.  
  
2.  Seleccione **los resultados de permanencia** opción. En el proceso de permanencia, DQS determina un registro de permanencia para cada clúster según la **regla de permanencia** que ha seleccionado.  
  
3.  Haga clic en **examinar** y navegue hasta la carpeta donde desea almacenar el archivo de salida.  
  
4.  Tipo **Cleansed and Matched Suppliers.xls** para el nombre y haga clic en **abierto**.  
  
5.  Confirme que **registro dinámico** está seleccionada para la **regla de permanencia**. Al seleccionar esta opción, se elige el registro dinámico de cada clúster para la salida de un clúster. Las demás opciones de la regla de supervivencia son las siguientes:  
  
    1.  **Registro más completo:** el registro de permanencia es el que tiene el mayor número de campos rellenos.  
  
    2.  **Registro más largo:** el registro de permanencia es el que tiene el mayor número de términos en campos de origen.  
  
    3.  **Registro más completo y más largo:** el registro de permanencia es el que tiene el mayor número de campos rellenos y con el mayor número de términos en cada campo.  
  
     ![Exportar los resultados de la página coincidencia](../../2014/tutorials/media/et-exportingtheresultsfrommatoanexcelfile.jpg "exportar los resultados de la página coincidencia")  
  
6.  Haga clic en **exportar** para exportar los resultados a un archivo de Excel.  
  
7.  Haga clic en **cerrar** para cerrar el **exportación de coincidencia** cuadro de diálogo.  
  
8.  Haga clic en **finalizar** para finalizar la actividad de coincidencia.  
  
9. Abra el **Cleansed and Matched Suppliers.xlsx** de archivo y confirme que no ve ningún duplicado (SupplierID).  
  
 Ahora, tiene datos de proveedor que se han limpiado y en el que se han buscado coincidencias para quitar valores duplicados.  
  
## <a name="next-step"></a>Paso siguiente  
 [Lección 4: Almacenar datos de proveedor en MDS](../../2014/tutorials/lesson-4-storing-supplier-data-in-mds.md)  
  
  
