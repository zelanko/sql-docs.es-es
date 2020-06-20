---
title: 'Paso 9: Probar el paquete del tutorial de la lección 1 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 9aee7acf-797b-46f2-830d-80ab64a9f0b6
author: janinezhang
ms.author: janinez
ms.openlocfilehash: fb4558d092daffc4a043d05b53a2d669f9cd66f1
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84966106"
---
# <a name="step-9-testing-the-lesson-1-tutorial-package"></a>Paso 9: Prueba del paquete del tutorial de la lección 1
  En esta lección, ha llevado a cabo las tareas siguientes:  
  
-   Ha creado un proyecto de [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
-   Ha configurado los administradores de conexión que el paquete necesita para conectarse a los datos de origen y de destino.  
  
-   Ha agregado un flujo de datos que toma los datos de un origen de archivo plano, realiza las transformaciones de búsqueda necesarias en los datos y configura los datos para el destino.  
  
 El paquete ya se ha completado. Ha llegado el momento de probarlo.  
  
## <a name="checking-the-package-layout"></a>Comprobar el diseño del paquete  
 Antes de probar el paquete, debe comprobar que los flujos de datos y de control de la lección 1 contienen los objetos mostrados en los diagramas siguientes.  
  
 **Flujo de control**  
  
 ![Flujo de control del paquete](../../2014/tutorials/media/task9lesson1control.gif "Flujo de control del paquete")  
  
 **Flujo de datos**  
  
 ![Flujo de datos del paquete](../../2014/tutorials/media/task9lesson1data.gif "Flujo de datos del paquete")  
  
### <a name="to-run-the-lesson-1-tutorial-package"></a>Para ejecutar el paquete del tutorial de la lección 1  
  
1.  En el menú **Depurar**, haga clic en **Iniciar depuración**.  
  
     El paquete se ejecutará, dando lugar a la correcta inclusión de 1097 filas en la tabla de hechos **FactCurrency** de **AdventureWorksDW2012**.  
  
2.  Una vez que se haya completado la ejecución del paquete, en el menú **Depurar** , haga clic en **Detener depuración**.  
  
## <a name="next-lesson"></a>Lección siguiente  
 [Lección 2: Adición de bucles](../integration-services/lesson-2-adding-looping-with-ssis.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejecución de proyectos y paquetes](packages/run-integration-services-ssis-packages.md)  
  
  
