---
title: "Paso 9: Probar el paquete del Tutorial lección 1 | Documentos de Microsoft"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: integration-services
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 9aee7acf-797b-46f2-830d-80ab64a9f0b6
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: ca45e8e1ba02246eb5429bd7bfea125663f69f41
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="lesson-1-9---testing-the-lesson-1-tutorial-package"></a>Lección 1-9: probar el paquete del Tutorial lección 1
En esta lección, ha llevado a cabo las tareas siguientes:  
  
-   Ha creado un proyecto de [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
-   Ha configurado los administradores de conexión que el paquete necesita para conectarse a los datos de origen y de destino.  
  
-   Ha agregado un flujo de datos que toma los datos de un origen de archivo plano, realiza las transformaciones de búsqueda necesarias en los datos y configura los datos para el destino.  
  
El paquete ya se ha completado. Ha llegado el momento de probarlo.  
  
## <a name="checking-the-package-layout"></a>Comprobar el diseño del paquete  
Antes de probar el paquete, debe comprobar que los flujos de datos y de control de la lección 1 contienen los objetos mostrados en los diagramas siguientes.  
  
**Flujo de control**  
  
![Controlar el flujo de paquete](../integration-services/media/task9lesson1control.gif "controlar el flujo del paquete")  
  
**Flujo de datos**  
  
![Flujo de datos en el paquete](../integration-services/media/task9lesson1data.gif "en paquete de flujo de datos")  
  
### <a name="to-run-the-lesson-1-tutorial-package"></a>Para ejecutar el paquete del tutorial de la lección 1  
  
1.  En el menú **Depurar** , haga clic en **Iniciar depuración**.  
  
    El paquete se ejecutará, dando lugar a la correcta inclusión de 1097 filas en la tabla de hechos **FactCurrency** de **AdventureWorksDW2012**.  
  
2.  Una vez que se haya completado la ejecución del paquete, en el menú **Depurar** , haga clic en **Detener depuración**.  
  
## <a name="next-lesson"></a>Lección siguiente  
[Lección 2: Agregar bucles con SSIS](../integration-services/lesson-2-adding-looping-with-ssis.md)  
  
## <a name="see-also"></a>Vea también  
[Ejecución de proyectos y paquetes](https://msdn.microsoft.com/library/ms141708(v=sql.110).aspx) 
  
  
  

