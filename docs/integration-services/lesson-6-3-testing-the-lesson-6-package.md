---
title: 'Paso 3: Probar el paquete de la lección 6 | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: c184c92d-948f-4037-a502-5fabd909c84c
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5119aef360778030f076a3e186225933b4a811a3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47796528"
---
# <a name="lesson-6-3---testing-the-lesson-6-package"></a>Lección 6-3: Probar el paquete de la lección 6
En tiempo de ejecución, el paquete obtendrá el valor de la Propiedad de directorio desde el parámetro VarFolderName.  
  
Para comprobar que, durante la ejecución, el paquete actualiza la propiedad Directory con el nuevo valor, simplemente debe ejecutar el paquete. Puesto que en el directorio solamente se copiaron tres archivos de datos de ejemplo, el flujo de datos solamente se ejecutará tres veces, en lugar de repetirse a través de los 14 archivos de la carpeta original.  
  
## <a name="checking-the-package-layout"></a>Comprobar el diseño del paquete  
Antes de probar el paquete, debe comprobar que los flujos de datos y de control de la lección 6 contienen los objetos mostrados en los diagramas siguientes. El flujo de control debe ser idéntico al flujo de datos de la lección 5. El flujo de datos debe ser idéntico al flujo de datos de la lección 5.  
  
**Flujo de control**  
  
![Flujo de control](../integration-services/media/task3lesson6control.jpg "Flujo de control")  
  
**Flujo de datos**  
  
![Flujo de datos](../integration-services/media/task3lesson6data.jpg "Flujo de datos")  
  
### <a name="to-test-the-lesson-6-tutorial-package"></a>Para probar el paquete del tutorial de la lección 6  
  
1.  En el menú Depurar, haga clic en Iniciar depuración.  
  
2.  Una vez que se haya completado la ejecución del paquete, en el menú Depurar, haga clic en Detener depuración.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
[Paso 4: implementar el paquete de la lección 6](../integration-services/lesson-6-4-deploying-the-lesson-6-package.md)  
  
  
  
