---
title: 'Paso 9: Probar el paquete del Tutorial de la lección 1 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 9aee7acf-797b-46f2-830d-80ab64a9f0b6
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 566284668ac8ea27aded665da7028375d97623e8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62767617"
---
# <a name="step-9-testing-the-lesson-1-tutorial-package"></a>Paso 9: Probar el paquete del Tutorial de la lección 1
  En esta lección, ha llevado a cabo las tareas siguientes:  
  
-   Ha creado un proyecto de [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
-   Ha configurado los administradores de conexión que el paquete necesita para conectarse a los datos de origen y de destino.  
  
-   Ha agregado un flujo de datos que toma los datos de un origen de archivo plano, realiza las transformaciones de búsqueda necesarias en los datos y configura los datos para el destino.  
  
 El paquete ya se ha completado. Ha llegado el momento de probarlo.  
  
## <a name="checking-the-package-layout"></a>Comprobar el diseño del paquete  
 Antes de probar el paquete, debe comprobar que los flujos de datos y de control de la lección 1 contienen los objetos mostrados en los diagramas siguientes.  
  
 **Flujo de control**  
  
 ![Flujo de control del paquete](../../2014/tutorials/media/task9lesson1control.gif "Control flow in package")  
  
 **Flujo de datos**  
  
 ![Flujo de datos del paquete](../../2014/tutorials/media/task9lesson1data.gif "Data flow in package")  
  
### <a name="to-run-the-lesson-1-tutorial-package"></a>Para ejecutar el paquete del tutorial de la lección 1  
  
1.  En el menú **Depurar** , haga clic en **Iniciar depuración**.  
  
     El paquete se ejecutará, dando lugar a la correcta inclusión de 1097 filas en la tabla de hechos **FactCurrency** de **AdventureWorksDW2012**.  
  
2.  Una vez que se haya completado la ejecución del paquete, en el menú **Depurar** , haga clic en **Detener depuración**.  
  
## <a name="next-lesson"></a>Lección siguiente  
 [Lección 2: Agregar bucles](../integration-services/lesson-2-adding-looping-with-ssis.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejecución de proyectos y paquetes](packages/run-integration-services-ssis-packages.md)  
  
  
