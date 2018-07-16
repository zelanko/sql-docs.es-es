---
title: 'Tarea 17: Revisar el proyecto de limpieza de DQS creado por el paquete SSIS | Microsoft Docs'
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
ms.topic: conceptual
ms.assetid: fc6cc258-72f5-4593-8edb-9f5bc66de9db
caps.latest.revision: 6
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 63d715ae86464a3d9411296fe8ffdfab155bab38
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37308845"
---
# <a name="task-17-reviewing-dqs-cleansing-project-created-by-the-ssis-package"></a>Tarea 17: revisar el proyecto de limpieza de DQS creado por el paquete SSIS
  En esta tarea, abrirá el proyecto de DQS creado por el paquete SSIS en el Cliente DQS, revisará los resultados del proceso de limpieza y, opcionalmente, realizará una limpieza interactiva y exportará los resultados.  
  
1.  Iniciar **Data Quality Client**.  
  
2.  Haga clic en **supervisión de la actividad** en el **administración** panel.  
  
3.  Ordenar la lista según **hora de inicio de la actividad** para ver el registro más reciente.  
  
4.  Tenga en cuenta que ve el nombre del proyecto en el siguiente formato: **CleanseAndCurate.Cleanse Supplier Data.GUID**.  
  
     ![Proyecto de limpieza de DQS creado por paquete SSIS](../../2014/tutorials/media/et-reviewingdqscpcreatedbythessispackage.jpg "proyecto de limpieza de DQS creado por paquete SSIS")  
  
5.  Tenga en cuenta que el valor de la **activa** campo es **Active**.  
  
6.  Haga clic en **Profiler** ficha en el panel inferior para ver las estadísticas del generador de perfiles para la actividad de limpieza que realizó el paquete SSIS.  
  
7.  Haga clic en **cerrar** para cerrar el **administración** pantalla.  
  
8.  En la página principal de **cliente DQS**, haga clic en **Abrir proyecto de calidad de datos** en el **proyectos de calidad de datos** panel.  
  
9. En la lista de proyectos, seleccione el proyecto creado por el componente Limpieza de DQS de SSIS. El nombre del proyecto debe tener el formato: **CleanseAndCurate.Cleanse Supplier Data.GUID (en color rojo)**. Es posible que deba ordenar la lista según **fecha de creación** columna y buscar el registro más reciente.  
  
10. Haga clic en **Siguiente**.  
  
11. El **administrar y ver resultados** página debería ser familiar por la limpieza interactiva que realizó anteriormente en este tutorial.  
  
12. Revise los resultados de la limpieza. También puede hacer una limpieza interactiva y exportar los resultados a un archivo de Excel o a una base de datos en la página siguiente.  
  
13. Haga clic en **Siguiente**. En este **exportar** página, puede exportar los resultados a un archivo de excel, el archivo CSV, o a una base de datos SQL.  
  
14. Haga clic en **finalizar** para finalizar la actividad.  
  
15. En la página principal de **cliente DQS**, haga clic en **supervisión de la actividad** en el **administración** panel.  
  
16. Tenga en cuenta que el valor de **IsActive** campo para el proyecto está **terminado** ahora.  
  
## <a name="next-step"></a>Paso siguiente  
 [Conclusión](../../2014/tutorials/conclusion.md)  
  
  
