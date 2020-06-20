---
title: Definir una variable de estado | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 45d66152-883a-49a7-a877-2e8ab45f8f79
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 6bdb65c464e63f8e7ab248c49f6dca729add3004
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84915995"
---
# <a name="define-a-state-variable"></a>Definir una variable de estado
  Este procedimiento describe cómo definir una variable de paquete donde se almacena el estado CDC.  
  
 La tarea Control CDC carga, inicializa y actualiza la variable de estado CDC y el componente de flujo de datos de origen de CDC la usa para determinar el intervalo de procesamiento actual de los registros de cambios. La variable de estado CDC se puede definir en cualquier contenedor común a la tarea Control CDC y al origen de CDC. Esto puede darse en el nivel de paquete pero también en otros contenedores, por ejemplo, en un contenedor de bucles.  
  
 No es aconsejable modificar de modo manual el valor de la variable de estado CDC, aunque puede ser útil conocer su contenido.  
  
 La siguiente tabla proporciona una descripción detallada de los componentes del valor de la variable de estado CDC.  
  
|Componente|Descripción|  
|---------------|-----------------|  
|`<state-name>`|Este es el nombre del estado CDC actual.|  
|`CS`|Esto marca el punto inicial del intervalo de procesamiento actual (inicio actual).|  
|`<cs-lsn>`|Este es el último LSN (número de secuencia de registro) procesado en la anterior ejecución de CDC.|  
|`CE`|Esto marca el punto final del intervalo de procesamiento actual (final actual). La presencia del componente CE en el estado CDC indica que, o bien se está procesando actualmente un paquete CDC, o un paquete CDC generó un error antes de procesar completamente su intervalo de procesamiento de CDC.|  
|`<ce-lsn>`|Este es el último LSN que se va a procesar en la ejecución de CDC actual. Se da siempre por supuesto que el último número de secuencia que se va a procesar es el máximo (0xFFF…).|  
|`IR`|Esto marca el intervalo de procesamiento inicial.|  
|`<ir-start>`|Este es un LSN de un cambio justo antes de que comenzara la carga inicial.|  
|`<ir-end>`|Este es un LSN de un cambio justo después de que finalizara la carga inicial.|  
|`TS`|Esto establece la marca de tiempo para la última actualización del estado CDC.|  
|**\<timestamp>**|Esta es una representación decimal de la propiedad System.DateTime.UtcNow de 64 bits.|  
|`ER`|Esto aparece si la última operación generó un error e incluye una breve descripción de la causa de este. Si este componente está presente, siempre aparecerá el último.|  
|`<short-error-text>`|Esta es la descripción breve del error.|  
  
 Los LSN y los números de secuencia se codifican como cadenas hexadecimales de hasta 20 dígitos que representan el valor LSN de Binary(10).  
  
 En la tabla siguiente se describen los valores de estado CDC posibles.  
  
|State|Descripción|  
|-----------|-----------------|  
|(INITIAL)|Este es el estado inicial antes de que se ejecute ningún paquete en el grupo CDC actual. Es también el estado cuando el estado CDC está vacío.|  
|ILSTART (Carga inicial iniciada)|Es el estado en el que se inicia el paquete de carga inicial, después de que la operación `MarkInitialLoadStart` llame a la tarea Control CDC.|  
|ILEND (Carga inicial terminada)|Es el estado en el que finaliza correctamente el paquete de carga inicial, después de que la operación `MarkInitialLoadEnd` llame a la tarea Control CDC.|  
|ILUPDATE (Actualización de carga inicial)|Es el estado en las ejecuciones del paquete de actualización de fuente de generación tras la carga inicial, mientras continúa procesándose el intervalo de procesamiento inicial. Es el estado después de que la operación `GetProcessingRange` llame a la tarea Control CDC.<br /><br /> Si se usa la columna __$reprocessing, se establece en 1 para indicar que el paquete puede estar ya volviendo a procesar filas en el destino.|  
|TFEND (Actualización de fuente de generación terminada)|Es el estado que se espera para las ejecuciones normales de CDC. Indica que la ejecución anterior se completó correctamente y que se puede iniciar una ejecución nueva con un intervalo de procesamiento nuevo.|  
|TFSTART|Es el estado que existe en una ejecución posterior del paquete de actualización de fuente de generación, tras la llamada de la operación `GetProcessingRange` a la tarea Control CDC.<br /><br /> Esto indica que se ha iniciado una ejecución de CDC normal correctamente, pero que no ha terminado aún (`MarkProcessedRange`).|  
|TFREDO (Reprocesamiento de actualizaciones de fuente de generación)|Es el estado en una `GetProcessingRange` que tiene lugar tras TFSTART. Esto indica que la ejecución anterior no ha finalizado correctamente.<br /><br /> Si se usa la columna __$reprocessing, se establece en 1 para indicar que el paquete puede estar ya volviendo a procesar filas en el destino.|  
|ERROR|El grupo CDC tiene un estado ERROR.|  
  
 Estos son algunos ejemplos de valores de la variable de estado CDC.  
  
-   ILSTART/IR/0x0000162B158700000000//TS/2011-08-07T17:10:43.0031645/  
  
-   ILSTART/IR/0x0000162B158700000000//TS/2011-08-07T17:10:43.0031645/  
  
-   TFEND/CS/0x0000025B000001BC0003/TS/2011-07-17T12:05:58.1001145/  
  
-   TFSTART/CS/0x0000030D000000AE0003/CE/0x0000159D1E0F01000000/TS/2011-08-09T05:30:43.9344900/  
  
-   TFREDO/CS/0x0000030D000000AE0003/CE/0x0000159D1E0F01000000/TS/2011-08-09T05:30:59.5544900/  
  
### <a name="to-define-a-cdc-state-variable"></a>Para definir una variable de estado CDC  
  
1.  En [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], abra el paquete de [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] que tenga el flujo CDC donde debe definir la variable.  
  
2.  Haga clic en la pestaña **Explorador de paquetes** y agregue una nueva variable.  
  
3.  Asigne a la variable un nombre que pueda reconocer como su variable de estado.  
  
4.  Proporcione a la variable de un tipo de datos **String** .  
  
 No proporcione a la variable un valor como parte de su definición. El valor debe ser establecido por la tarea Control CDC.  
  
 Si piensa usar la tarea Control CDC con **Persistencia automática de estado**, la variable de estado CDC se leerá de la tabla de estado de la base de datos que especifique y se actualizará en la misma tabla cuando su valor cambie. Para obtener más información acerca de la tabla de estado, vea [CDC Control Task](../control-flow/cdc-control-task.md)y [CDC Control Task Editor](../cdc-control-task-editor.md).  
  
 Si no usa la tarea Control CDC con la persistencia automática de estado, debe cargar el valor de la variable del almacenamiento persistente donde se guardó su valor la última vez que el paquete se ejecutó y escribirlo de nuevo en el almacenamiento persistente cuando procesamiento del intervalo de procesamiento actual se complete.  
  
## <a name="see-also"></a>Consulte también  
 [Tarea control CDC](../control-flow/cdc-control-task.md)   
 [Editor de la tarea Control de CDC](../cdc-control-task-editor.md)  
  
  
