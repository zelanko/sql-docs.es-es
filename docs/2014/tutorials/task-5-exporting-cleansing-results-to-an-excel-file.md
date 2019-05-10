---
title: 'Tarea 5: Exportar los resultados a un archivo de Excel de la limpieza | Microsoft Docs'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: eaeafd65-d0d4-4a7d-a3ad-110ef644e90b
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 3c690becefb71b71c154131b6957c1063872b540
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/09/2019
ms.locfileid: "65489125"
---
# <a name="task-5-exporting-cleansing-results-to-an-excel-file"></a>Tarea 5: Exportación de los resultados de la limpieza a un archivo de Excel
  En esta tarea, exportará los resultados de la actividad de limpieza a un archivo de Excel. Consulte [fase de exportación](https://msdn.microsoft.com/library/hh213061.aspx#Export) tema para obtener más detalles.  
  
1.  En el panel derecho, seleccione **Excel** para el **tipo de destino**.  
  
2.  Haga clic en **examinar**, especifique el nombre de archivo de salida como **Cleansed Supplier List.xls**y, a continuación, haga clic en **abierto**.  
  
3.  Seleccione **solo datos** para el **salida** formato para exportar solo los datos limpios. La segunda opción, **datos e información de limpieza**, le permite exportar los detalles de actividad de limpieza junto con los datos limpios. El **estandarizar** opción le permite aplicar cualquier formato de salida se define en un dominio a los valores de ese dominio. En el tutorial no ha definido ningún formato de salida en ningún dominio.  
  
     ![Página de resultados de limpieza de exportación](../../2014/tutorials/media/et-exportingcleansingresultstoanexcelfile.jpg "página de resultados de limpieza de exportación")  
  
4.  Haga clic en **exportar** para exportar los datos. Haga clic en no **finalizar** todavía.  
  
5.  Haga clic en **cerrar** en el **exportar** cuadro de diálogo.  
  
6.  Haga clic en **finalizar** para finalizar la actividad. Si olvidó exportar los resultados antes de hacer clic **finalizar**, haga clic en **Abrir proyecto de calidad de datos** en la página principal de **cliente DQS**, seleccione **proveedor limpiar Lista** en la lista de proyectos y haga clic en **siguiente** en la parte inferior de la pantalla para llegar a la **exportar** fase del proceso de limpieza de nuevo. También puede cambiar a **administrar y ver resultados** ficha haciendo **volver** botón.  
  
7.  Abra el **Cleansed Supplier List.xls** y realice lo siguiente:  
  
    1.  Asegúrese de que no hay ninguna dirección de correo electrónico que terminen en adventure-work.com (del carácter ') mediante la búsqueda de adventure-work.com en la hoja de cálculo.  
  
    2.  Vea que no haya ningún **EE.UU.** valor en el **país** columna.  
  
    3.  Busque **Los Ángeles** y verá que el **estado** está establecido en **CA**.  
  
    4.  Confirme que no hay ningún término **Co.**, **Corp.**, y **Inc.**.  
  
    5.  Eliminar el **validación de direcciones** columna de la hoja de cálculo y guarde el archivo de excel. Esta columna adicional corresponde al dominio de compuesto Validación de direcciones.  
  
## <a name="next-step"></a>Paso siguiente  
 [Tarea 6: Importar valores desde el proveedor proyecto limpiar lista](../../2014/tutorials/task-6-importing-values-from-the-cleanse-supplier-list-project.md)  
  
  
