---
title: 'Paso 3: Probar el paquete de la lección 6 | Microsoft Docs'
ms.custom: ''
ms.date: 01/11/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: c184c92d-948f-4037-a502-5fabd909c84c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 001ba5fc56393cbbcdbc8b5379abc8390dc05e0a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65721238"
---
# <a name="lesson-6-3-test-the-lesson-6-package"></a>Lección 6-3: Probar el paquete de la lección 6

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


En tiempo de ejecución, el paquete obtiene el valor de la propiedad **Directory** del parámetro **VarFolderName**.  
  
Para comprobar que el paquete actualiza la propiedad **Directory**, ejecute el paquete. Dado que ha copiado tres archivos de datos de ejemplo en el nuevo directorio, el flujo de datos se ejecuta tres veces.
  
## <a name="check-the-package-layout"></a>Comprobación del diseño del paquete  
Antes de probar el paquete, compruebe que los flujos de datos y de control del paquete de la lección 6 son similares a los objetos mostrados en los diagramas siguientes:   
  
**Flujo de control**  
  
![Flujo de control](../integration-services/media/task4lesson2control.gif "Flujo de control")  
  
**Flujo de datos**  
  
![Flujo de datos](../integration-services/media/task5lesson5data.gif "Flujo de datos")  
  
## <a name="test-the-lesson-6-package"></a>Probar el paquete de la lección 6  
  
1.  En el menú **Depurar**, seleccione **Iniciar depuración**.  
  
2.  Una vez que se haya completado la ejecución del paquete, en el menú **Depurar**, seleccione **Detener depuración**.  
  
## <a name="go-to-next-task"></a>Ir a la tarea siguiente
[Paso 4: Implementar el paquete de la lección 6](../integration-services/lesson-6-4-deploying-the-lesson-6-package.md)  
  
  
  
