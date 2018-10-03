---
title: 'Paso 4: Probar el paquete del tutorial de la lección 5 | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 5215b77d-c2ec-4b25-a3de-ca49ea197d74
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 3f23e1e6e9321d4211c53a176242c81cad6ff8bb
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47664563"
---
# <a name="lesson-5-4---testing-the-lesson-5-tutorial-package"></a>Lección 5-4: Probar el paquete del tutorial de la lección 5
Durante la ejecución, el paquete obtendrá el valor de la propiedad **Directory** de una variable actualizada en tiempo de ejecución, en lugar de utilizar el nombre de directorio original especificado al crear el paquete. El valor de la variable lo rellena el archivo SSISTutorial.dtsConfig.  
  
Para comprobar que, durante la ejecución, el paquete actualiza la propiedad Directory con el nuevo valor, simplemente debe ejecutar el paquete. Puesto que en el directorio solamente se copiaron tres archivos de datos de ejemplo, el flujo de datos solamente se ejecutará tres veces, en lugar de repetirse a través de los 14 archivos de la carpeta original.  
  
## <a name="checking-the-package-layout"></a>Comprobar el diseño del paquete  
Antes de probar el paquete, debe comprobar que los flujos de datos y de control de la lección 5 contienen los objetos mostrados en los diagramas siguientes. El flujo de control debe ser idéntico al flujo de datos de la lección 4. El flujo de datos debe ser idéntico al flujo de datos de la lección 4.  
  
**Flujo de control**  
  
![Flujo de control del paquete](../integration-services/media/task4lesson2control.gif "Control flow in package")  
  
**Flujo de datos**  
  
![Flujo de datos del paquete](../integration-services/media/task9lesson1data.gif "Data flow in package")  
  
### <a name="to-test-the-lesson-5-tutorial-package"></a>Para probar el paquete de tutorial de la lección 5  
  
1.  En el menú **Depurar** , haga clic en **Iniciar depuración**.  
  
2.  Una vez que haya finalizado la ejecución del paquete, en el menú **Depurar** , haga clic en **Detener depuración**.  
  
## <a name="next-lesson"></a>Lección siguiente  
[Lección 6: Uso de parámetros con el modelo de implementación de proyectos en SSIS](../integration-services/lesson-6-using-parameters-with-the-project-deployment-model-in-ssis.md)  
  
  
  
