---
title: 'Tarea 5: Exportar los resultados a un archivo de Excel la limpieza | Documentos de Microsoft'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: eaeafd65-d0d4-4a7d-a3ad-110ef644e90b
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: f8a716d3b6c0007ceb89f36f23584bb4adb4f706
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36104374"
---
# <a name="task-5-exporting-cleansing-results-to-an-excel-file"></a>Tarea 5: exportar los resultados de la limpieza a un archivo de Excel
  En esta tarea, exportará los resultados de la actividad de limpieza a un archivo de Excel. Vea [fase de exportación](http://msdn.microsoft.com/library/hh213061.aspx#Export) tema para obtener más detalles.  
  
1.  En el panel derecho, seleccione **Excel** para el **tipo de destino**.  
  
2.  Haga clic en **examinar**, especifique el nombre de archivo de salida como **Cleansed Supplier List.xls**y, a continuación, haga clic en **abiertos**.  
  
3.  Seleccione **sólo los datos** para el **salida** formato para exportar solo los datos limpios. La segunda opción, **datos e información de limpieza**, permite exportar detalles de la actividad de limpieza junto con los datos limpios. El **estandarizar** opción le permite aplicar cualquier formato de salida que se defina en un dominio a los valores de ese dominio. En el tutorial no ha definido ningún formato de salida en ningún dominio.  
  
     ![Página de resultados de la exportación de limpieza](../../2014/tutorials/media/et-exportingcleansingresultstoanexcelfile.jpg "página de resultados de la exportación de limpieza")  
  
4.  Haga clic en **exportar** para exportar los datos. No haga clic en **finalizar** todavía.  
  
5.  Haga clic en **cerrar** en el **exportar** cuadro de diálogo.  
  
6.  Haga clic en **finalizar** para finalizar la actividad. Si ha olvidado exportar los resultados antes de hacer clic **finalizar**, haga clic en **Abrir proyecto de calidad de datos** en la página principal de **cliente DQS**, seleccione **proveedor limpiar Lista** en la lista de proyectos y haga clic en **siguiente** en la parte inferior de la pantalla para ayudarle a obtener el **exportar** fase del proceso de limpieza de nuevo. También puede cambiar a **administrar y ver resultados** ficha haciendo clic en **volver** botón.  
  
7.  Abra la **Cleansed Supplier List.xls** y realice lo siguiente:  
  
    1.  Asegúrese de que no haya direcciones de correo electrónico que terminen en adventure-work.com (sin el carácter 's'); para ello, busque adventure-work.com en la hoja de cálculo.  
  
    2.  Vea que no hay ningún **Estados Unidos** valor en el **país** columna.  
  
    3.  Busque **Los Ángeles** y compruebe que la **estado** está establecido en **CA**.  
  
    4.  Confirme que no hay ningún término **Co.**, **Corp.**, y **Inc.**.  
  
    5.  Eliminar el **validación de direcciones** columna de la hoja de cálculo y guarde el archivo de excel. Esta columna adicional corresponde al dominio de compuesto Validación de direcciones.  
  
## <a name="next-step"></a>Paso siguiente  
 [Tarea 6: Importar valores desde el proyecto de la lista de proveedores limpiar](../../2014/tutorials/task-6-importing-values-from-the-cleanse-supplier-list-project.md)  
  
  