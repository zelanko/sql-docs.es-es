---
title: 'Tarea 17: Revisar el proyecto de limpieza de DQS creado por el paquete SSIS | Documentos de Microsoft'
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: fc6cc258-72f5-4593-8edb-9f5bc66de9db
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 4226fd9a8e8eb8aa2851eed8eb318b8535010c8a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36200032"
---
# <a name="task-17-reviewing-dqs-cleansing-project-created-by-the-ssis-package"></a>Tarea 17: revisar el proyecto de limpieza de DQS creado por el paquete SSIS
  En esta tarea, abrirá el proyecto de DQS creado por el paquete SSIS en el Cliente DQS, revisará los resultados del proceso de limpieza y, opcionalmente, realizará una limpieza interactiva y exportará los resultados.  
  
1.  Iniciar **Data Quality Client**.  
  
2.  Haga clic en **supervisión de la actividad** en el **administración** panel.  
  
3.  Ordenar la lista en función de **hora de inicio de actividad** para ver el registro más reciente.  
  
4.  Observe que ve el nombre del proyecto en el siguiente formato: **CleanseAndCurate.Cleanse Supplier Data.GUID**.  
  
     ![Proyecto de limpieza de DQS creado por paquete SSIS](../../2014/tutorials/media/et-reviewingdqscpcreatedbythessispackage.jpg "proyecto de limpieza de DQS creado por paquete SSIS")  
  
5.  Tenga en cuenta que el valor de la **activa** campo es **Active**.  
  
6.  Haga clic en **Profiler** ficha en el panel inferior para ver las estadísticas del generador de perfiles para la actividad de limpieza que realizó el paquete SSIS.  
  
7.  Haga clic en **cerrar** para cerrar el **administración** pantalla.  
  
8.  En la página principal de **cliente DQS**, haga clic en **Abrir proyecto de calidad de datos** en el **proyectos de calidad de datos** panel.  
  
9. En la lista de proyectos, seleccione el proyecto creado por el componente Limpieza de DQS de SSIS. El nombre del proyecto debe estar en formato: **CleanseAndCurate.Cleanse Supplier Data.GUID (en color rojo)**. Debe ordenar la lista en función de **fecha de creación de** columna y buscar el registro más reciente.  
  
10. Haga clic en **Siguiente**.  
  
11. El **administrar y ver resultados** página debe resultarle familiar de la limpieza interactiva que realizó anteriormente en este tutorial.  
  
12. Revise los resultados de la limpieza. También puede hacer una limpieza interactiva y exportar los resultados a un archivo de Excel o a una base de datos en la página siguiente.  
  
13. Haga clic en **Siguiente**. En este **exportar** página, puede exportar los resultados a un archivo de excel, archivo CSV, o a una base de datos SQL.  
  
14. Haga clic en **finalizar** para finalizar la actividad.  
  
15. En la página principal de **cliente DQS**, haga clic en **supervisión de la actividad** en el **administración** panel.  
  
16. Tenga en cuenta que el valor de **IsActive** campo del proyecto es **finalizado** ahora.  
  
## <a name="next-step"></a>Paso siguiente  
 [Conclusión](../../2014/tutorials/conclusion.md)  
  
  