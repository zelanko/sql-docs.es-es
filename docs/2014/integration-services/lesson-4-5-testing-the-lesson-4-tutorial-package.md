---
title: 'Paso 5: Probar el paquete del tutorial de la lección 4 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 5f18df92-0248-4858-836b-c8b02f0e0439
caps.latest.revision: 22
author: douglaslM
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 10e6f1b123364f13c0132fb376794b9e37fdc96c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36106141"
---
# <a name="step-5-testing-the-lesson-4-tutorial-package"></a>Paso 5: Probar el paquete del tutorial de la lección 4
  En tiempo de ejecución, el archivo dañado, Currency_BAD.txt, no podrá generar una coincidencia en la transformación Lookup Currency Key. Puesto que la salida de errores de Lookup Currency Key se ha configurado para redirigir las filas con errores al nuevo destino de filas con errores, el componente no genera ningún error y el paquete se ejecuta correctamente. Todas las filas que generan un error se escriben en el archivo ErrorOutput.txt.  
  
 En esta tarea, probará la configuración de la salida de error revisada ejecutando el paquete. Tras ejecutar correctamente el paquete, verá el contenido del archivo ErrorOutput.txt.  
  
> [!NOTE]  
>  Si no desea acumular filas con errores en el archivo ErrorOutput.txt, debe eliminar manualmente el contenido del archivo entre ejecuciones de paquetes.  
  
## <a name="checking-the-package-layout"></a>Comprobar el diseño del paquete  
 Antes de probar el paquete, debe comprobar que los flujos de datos y de control del paquete de la lección 4 contienen los objetos mostrados en los diagramas siguientes. El flujo de control debe ser idéntico al flujo de datos de las lecciones 2 a 4.  
  
 **Flujo de control**  
  
 ![Flujo de control del paquete](../../2014/tutorials/media/task4lesson2control.gif "Control flow in package")  
  
 **Flujo de datos**  
  
 ![Flujo de datos del paquete](../../2014/tutorials/media/task5lesson5data.gif "Data flow in package")  
  
### <a name="to-run-the-lesson-4-tutorial-package"></a>Para ejecutar el paquete de tutorial de la lección 4  
  
1.  En el menú **Depurar** , haga clic en **Iniciar depuración**.  
  
2.  Una vez que se haya completado la ejecución del paquete, en el menú **Depurar** , haga clic en **Detener depuración**.  
  
### <a name="to-verify-the-contents-of-the-erroroutputtxt-file"></a>Para comprobar el contenido del archivo ErrorOutput.txt  
  
-   En el Bloc de notas o en cualquier otro editor de texto, abra el archivo ErrorOutput.txt. El orden predeterminado de las columnas es: AverageRate, CurrencyID, CurrencyDate, EndOfDateRate, ErrorCode, ErrorColumn, ErrorDescription.  
  
     Observe que todas las filas del archivo contienen el valor BAD de CurrencyID sin coincidencia, el valor -1071607778 de ErrorCode, el valor 0 de ErrorColumn y el valor "La fila no produjo ninguna coincidencia durante la búsqueda" de ErrorDescription. El valor de ErrorColumn se establece en 0 porque el error no es específico de columna. Es la operación de búsqueda la que ha generado el error. .  
  
  