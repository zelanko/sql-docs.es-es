---
title: 'Paso 9: Prueba del paquete del tutorial de la lección 1 | Microsoft Docs'
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 9aee7acf-797b-46f2-830d-80ab64a9f0b6
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ec7514eeb2e614c1313fba81c4a48b8803f0c29d
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2019
ms.locfileid: "71296090"
---
# <a name="lesson-1-9-test-the-lesson-1-package"></a>Lección 1-9: Prueba del paquete de la lección 1

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



En este tutorial, ha realizado las tareas siguientes:  
  
-   Ha creado un proyecto de [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
-   Ha configurado los administradores de conexiones para que el paquete se conecte a los datos de origen y de destino.  
  
-   Ha agregado un flujo de datos que toma los datos de un origen de archivo plano, realiza las transformaciones de búsqueda necesarias en los datos y configura los datos para el destino.  
  
El paquete ya se ha completado y está listo para probarse.
  
## <a name="check-the-package-components"></a>Comprobación de los componentes del paquete
  
Antes de probar el paquete, compruebe que los flujos de datos y de control del paquete de la lección 1 contienen los objetos mostrados en los diagramas siguientes.  
  
**Flujo de control** 
  
![Flujo de control del paquete](../integration-services/media/task9lesson1control.gif "Control flow in package")  
  
**Flujo de datos**  
  
![Flujo de datos del paquete](../integration-services/media/task9lesson1data.gif "Data flow in package")  
  
## <a name="run-the-lesson-1-package"></a>Ejecución del paquete de la lección 1  
  
1.  En el menú **Depurar**, seleccione **Iniciar depuración**.  
  
    El paquete se ejecuta y da lugar a la inclusión correcta de 1.097 filas en la tabla de hechos **NewFactCurrencyRate** de **AdventureWorksDW2012**. Para comprobar este resultado, haga clic en la pestaña **Flujo de datos**.
  
2.  Una vez que se haya completado la ejecución del paquete, en el menú **Depurar**, haga clic en **Detener depuración**.  
  
## <a name="go-to-next-lesson"></a>Ir a la lección siguiente
[Lección 2: Adición de bucles con SSIS](../integration-services/lesson-2-adding-looping-with-ssis.md)  
  
## <a name="see-also"></a>Vea también  
[Ejecución de proyectos y paquetes](packages/run-integration-services-ssis-packages.md) 
  
  
  
