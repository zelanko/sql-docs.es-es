---
title: 'Paso 5: Prueba del paquete del tutorial de la lección 4 | Microsoft Docs'
ms.custom: ''
ms.date: 01/07/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 5f18df92-0248-4858-836b-c8b02f0e0439
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 2725731d216b651d310b204f4cdf6b19612ae435
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68055810"
---
# <a name="lesson-4-5-test-the-lesson-4-package"></a>Lección 4-5: Prueba del paquete de la lección 4

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



En tiempo de ejecución, el archivo dañado **Currency_BAD.txt** no puede generar una coincidencia en la transformación de búsqueda Currency Key. Como la salida de errores de Currency Key Lookup se ha configurado para redirigir las filas con error al nuevo destino Failed Rows, el componente no genera ningún error y el paquete se ejecuta correctamente. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] escribe todas las filas con error en **ErrorOutput.txt**.  
  
En esta tarea, se prueba la configuración de la salida de error revisada mediante la ejecución del paquete. Después de ejecutar correctamente el paquete, verá el contenido del archivo **ErrorOutput.txt**.  
  
> [!NOTE]  
> Si no quiere acumular filas con errores en el archivo **ErrorOutput.txt**, elimine manualmente el contenido del archivo entre ejecuciones del paquete.  
  
## <a name="check-the-package-layout"></a>Comprobación del diseño del paquete  
Antes de probar el paquete, compruebe que los flujos de datos y de control del paquete de la lección 4 son similares a los diagramas siguientes: 
  
**Flujo de control**  
  
![Flujo de control del paquete](../integration-services/media/task4lesson2control.gif "Control flow in package")  
  
**Flujo de datos**  
  
![Flujo de datos del paquete](../integration-services/media/task5lesson5data.gif "Data flow in package")  
  
## <a name="run-the-lesson-4-tutorial-package"></a>Ejecución del paquete del tutorial de la lección 4  
  
1.  En el menú **Depurar**, seleccione **Iniciar depuración**.  
  
2.  Una vez que se haya completado la ejecución del paquete, en el menú **Depurar**, seleccione **Detener depuración**.  
  
## <a name="view-the-contents-of-the-erroroutputtxt-file"></a>Visualización del contenido del archivo ErrorOutput.txt  
  
En el Bloc de notas o en cualquier otro editor de texto, abra el archivo **ErrorOutput.txt**. El orden predeterminado de columna es: AverageRate, CurrencyID, CurrencyDate, EndOfDateRate, ErrorCode, ErrorColumn, ErrorDescription.  
 
Todas las filas del archivo contienen el valor "BAD" de CurrencyID sin coincidencia, el valor -1071607778 de ErrorCode, el valor 0 de ErrorColumn y el valor "La fila no produjo ninguna coincidencia durante la búsqueda" de ErrorDescription. El valor de ErrorColumn es 0 porque el error no es específico de la columna; no se ha podido realizar la operación de búsqueda.
  
  
## <a name="next-lesson"></a>Lección siguiente
[Lección 5: Adición de configuraciones de paquete de SSIS para el modelo de implementación de paquetes](../integration-services/lesson-5-add-ssis-package-configurations-for-the-package-deployment-model.md)  
