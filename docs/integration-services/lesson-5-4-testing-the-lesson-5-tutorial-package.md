---
description: 'Lección 5-4: Probar el paquete de la lección 5'
title: 'Paso 4: Probar el paquete de la lección 5 | Microsoft Docs'
ms.custom: ''
ms.date: 01/08/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 5215b77d-c2ec-4b25-a3de-ca49ea197d74
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 57bad9d0d13f85ae52858005e3fb6acc6f9532f0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500830"
---
# <a name="lesson-5-4-test-the-lesson-5-package"></a>Lección 5-4: Probar el paquete de la lección 5

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]



En tiempo de ejecución, el paquete obtiene el valor de la propiedad **Directory** de una variable de configuración, en lugar de hacerlo del nombre de directorio especificado al crear el paquete. El valor de la variable proviene del archivo XML **SSISTutorial.dtsConfig**.  
  
Para comprobar que el paquete actualiza la propiedad **Directory** con el nuevo valor durante el tiempo de ejecución, ejecute el paquete. Dado que solo hay tres archivos de datos de ejemplo en el nuevo directorio, el flujo de datos solo se ejecuta tres veces.  
  
## <a name="checking-the-package-layout"></a>Comprobar el diseño del paquete  
Antes de probar el paquete, compruebe que los flujos de datos y de control del paquete de la lección 5 son similares a los objetos mostrados en los diagramas siguientes:  
  
**Flujo de control**  
  
![Flujo de control del paquete](../integration-services/media/task4lesson2control.gif "Flujo de control del paquete")  
  
**Flujo de datos**  
  
![Flujo de datos del paquete](../integration-services/media/task9lesson1data.gif "Flujo de datos del paquete")  
  
## <a name="test-the-lesson-5-package"></a>Probar el paquete de la lección 5  
  
1.  En el menú **Depurar**, seleccione **Iniciar depuración**.  
  
2.  Una vez que se haya completado la ejecución del paquete, en el menú **Depurar**, seleccione **Detener depuración**.  
  
## <a name="next-lesson"></a>Lección siguiente  
[Lección 6: Uso de parámetros con el modelo de implementación de proyectos en SSIS](../integration-services/lesson-6-using-parameters-with-the-project-deployment-model-in-ssis.md)  
  
  
  
