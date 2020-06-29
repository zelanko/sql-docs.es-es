---
title: 'Paso 4: Probar el paquete del tutorial de la lección 5 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 5215b77d-c2ec-4b25-a3de-ca49ea197d74
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f7fcaa0ecab3561e49fc8080251d2523034f5149
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2020
ms.locfileid: "85440382"
---
# <a name="step-4-testing-the-lesson-5-tutorial-package"></a>Paso 4: Prueba del paquete del tutorial de la lección 5
  Durante la ejecución, el paquete obtendrá el valor de la propiedad `Directory` de una variable actualizada en tiempo de ejecución, en lugar de utilizar el nombre de directorio original especificado al crear el paquete. El valor de la variable lo rellena el archivo SSISTutorial.dtsConfig.  
  
 Para comprobar que, durante la ejecución, el paquete actualiza la propiedad Directory con el nuevo valor, simplemente debe ejecutar el paquete. Puesto que en el directorio solamente se copiaron tres archivos de datos de ejemplo, el flujo de datos solamente se ejecutará tres veces, en lugar de repetirse a través de los 14 archivos de la carpeta original.  
  
## <a name="checking-the-package-layout"></a>Comprobar el diseño del paquete  
 Antes de probar el paquete, debe comprobar que los flujos de datos y de control de la lección 5 contienen los objetos mostrados en los diagramas siguientes. El flujo de control debe ser idéntico al flujo de datos de la lección 4. El flujo de datos debe ser idéntico al flujo de datos de la lección 4.  
  
 **Flujo de control**  
  
 ![Flujo de control del paquete](../../2014/tutorials/media/task4lesson2control.gif "Flujo de control del paquete")  
  
 **Flujo de datos**  
  
 ![Flujo de datos del paquete](../../2014/tutorials/media/task9lesson1data.gif "Flujo de datos del paquete")  
  
### <a name="to-test-the-lesson-5-tutorial-package"></a>Para probar el paquete de tutorial de la lección 5  
  
1.  En el menú **Depurar**, haga clic en **Iniciar depuración**.  
  
2.  Una vez finalizada la ejecución del paquete, en el menú **depurar** , haga clic en **detener depuración**.  
  
## <a name="next-lesson"></a>Lección siguiente  
 [Lección 6: Uso de parámetros con el modelo de implementación de proyectos](../integration-services/lesson-6-using-parameters-with-the-project-deployment-model-in-ssis.md)  
  
  
