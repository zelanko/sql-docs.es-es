---
title: "Procesamiento de opciones y configuración (Analysis Services) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- process data option [Analysis Services]
- processing objects [Analysis Services]
- unprocess option [Analysis Services]
- process full option [Analysis Services]
- process index option [Analysis Services]
- process structure option [Analysis Services]
- process incremental option [Analysis Services]
- process update option [Analysis Services]
- process clear structure option [Analysis Services]
- process default option [Analysis Services]
ms.assetid: 2e858c74-ad3e-45f1-8745-efe2c0c3a7fa
caps.latest.revision: "48"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 37311ad6191047a4eebdc51f427bc0e28c8f86d0
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="processing-options-and-settings-analysis-services"></a>Opciones y valores de procesamiento (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Si procesa objetos en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], puede seleccionar una opción de procesamiento para controlar el tipo de procesamiento que se produce para cada objeto. Los tipos de procesamiento difieren entre objetos y por los cambios producidos en el objeto debido a su último procesamiento. Si habilita [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para seleccionar automáticamente un método de procesamiento, el programa utilizará el método que devuelve el objeto a un estado totalmente procesado en el menor tiempo posible.  
  
 La configuración de procesamiento permite controlar los objetos que se procesan y los métodos que se utilizan para procesar dichos objetos. Algunas configuraciones de procesamiento se utilizan principalmente por trabajos de procesamiento por lotes. Para más información sobre el procesamiento por lotes, vea [Procesamiento por lotes &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/batch-processing-analysis-services.md).  
  
> [!NOTE]  
>  Este tema se aplica a las soluciones multidimensionales y de minería de datos. Para más información sobre las soluciones tabulares, vea [Procesar base de datos, tabla o partición &#40;Analysis Services&#41;](../../analysis-services/tabular-models/process-database-table-or-partition-analysis-services.md).  
  
## <a name="processing-options"></a>Opciones de procesamiento  
 En la siguiente tabla se describen los métodos de procesamiento disponibles en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]y se identifican los objetos compatibles con cada método.  
  
|Modo|Se aplica a|Description|  
|----------|----------------|-----------------|  
|**Proceso predeterminado**|Cubos, bases de datos, dimensiones, grupos de medida, modelos de minería de datos, estructuras de minería de datos y particiones.|Detecta el estado de proceso de los objetos de base de datos y realiza el procesamiento necesario para devolver objetos sin procesar o procesados parcialmente a un estado de procesamiento completo. Si cambia un enlace de datos, el Proceso predeterminado realizará un Proceso completo en el objeto afectado.|  
|**Proceso completo**|Cubos, bases de datos, dimensiones, grupos de medida, modelos de minería de datos, estructuras de minería de datos y particiones.|Procesa un objeto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y todos los objetos que contiene. Cuando se ejecuta Proceso completo en un objeto que ya se ha procesado, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] quita todos los datos del objeto y, a continuación, lo procesa. Este tipo de procesamiento es necesario cuando se ha realizado un cambio estructural en un objeto; por ejemplo, cuando se agrega, se elimina o se cambia el nombre de una jerarquía de atributo.|  
|**Procesar borrado**|Cubos, bases de datos, dimensiones, grupos de medida, modelos de minería de datos, estructuras de minería de datos y particiones.|Quita los datos del objeto especificado y de cualquier otro objeto que forme parte de un nivel inferior. Los datos no se vuelven a cargar una vez quitados.|  
|**Procesar datos**|Dimensiones, cubos, grupos de medida y particiones.|Procesa solo los datos sin generar agregaciones ni índices. Si existen datos en las particiones, se quitarán antes de volver a rellenar la partición con los datos de origen.|  
|**Procesar adición**|Dimensiones, grupos de medida y particiones.<br /><br /> Nota: **Procesar Agregar** no está disponible para el procesamiento de dimensiones en [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], pero puede escribir el script XMLA para realizar esta acción.|En el caso de dimensiones, agrega nuevos miembros y actualiza títulos y descripciones de atributos de dimensión.<br /><br /> En el caso de grupos de medida y particiones, agrega nuevos datos de hechos disponibles y procesa solo las particiones relevantes.|  
|**Procesar actualización**|Dimensions|Impone un relectura de los datos y una actualización de atributos de dimensión. Se quitarán las agregaciones flexibles y los índices de las particiones relacionadas.|  
|**Procesar índice**|Cubos, dimensiones, grupos de medida y particiones|Crea o regenera índices y agregaciones para todas las particiones procesadas. En el caso de objetos sin procesar, esta opción genera un error.<br /><br /> El procesamiento con esta opción se necesita si se desactiva el Procesamiento diferido.|  
|**Procesar estructura**|Cubos y estructuras de minería de datos|Si se cancela el proceso del cubo, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] procesa todas las dimensiones del cubo, si es necesario. Después, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] creará solo definiciones de cubo. Si esta opción se aplica a una estructura de minería de datos, la rellena con los datos de origen. La diferencia entre esta opción y la opción Process Full consiste en que esta opción no itera el procesamiento hasta llegar a los modelos de minería de datos.|  
|**Procesar borrado de estructura**|Estructuras de minería de datos|Quita todos los datos de entrenamiento de una estructura de minería de datos.|  
  
## <a name="processing-settings"></a>Configuración de procesamiento  
 En la siguiente tabla se describen las configuraciones de procesamiento disponibles cuando se crea una operación de proceso.  
  
|Opción de procesamiento|Description|Valor de la opción|  
|-----------------------|-----------------|------------------|  
|**Parallel**|Se utiliza para el procesamiento por lotes. Esta configuración hace que [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] bifurque las tareas de procesamiento para ejecutarlas en paralelo en una sola transacción. Si se produce un error, se revertirán todos los cambios. Puede establecer el número máximo de tareas en paralelo explícitamente, o bien dejar que el servidor decida la distribución óptima. La opción Paralelas permite obtener un procesamiento más rápido.||  
|**Secuenciales (modo de transacción)**|Controla el comportamiento de ejecución del trabajo de procesamiento. Hay dos opciones disponibles:<br /><br /> Cuando se realiza el proceso utilizando **Una transacción**, se confirman todos los cambios una vez que se realiza correctamente el trabajo de procesamiento. Esto significa que todos los objetos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] afectados por un trabajo de procesamiento concreto permanecen disponibles para consultas hasta el proceso de confirmación. De esta manera, los objetos no están disponibles temporalmente. El uso de **Transacciones independientes** hace que todos los objetos afectados por un proceso en el trabajo de procesamiento no estén disponibles para consultas en cuanto dicho proceso se lleva a cabo correctamente.|**Una transacción**. El trabajo de procesamiento se ejecuta como una transacción. Si se llevan a cabo correctamente todos los procesos de un trabajo de procesamiento, se confirman todos los cambios realizados por el trabajo de procesamiento. Si un proceso falla, se revierten todos los cambios realizados por el trabajo de procesamiento. **Una transacción** es el valor predeterminado.<br /><br /> **Transacciones independientes**. Cada proceso en el trabajo de procesamiento se ejecuta como un trabajo independiente. Si falla un proceso, solamente se revierte ese proceso y el trabajo de procesamiento continúa. Cada trabajo confirma todos los cambios del proceso al final del trabajo.|  
|**Opción de tabla de reescritura**|Controla el modo en que se administran las tablas de reescritura durante el procesamiento. Esta opción se aplica a las particiones de reescritura de un cubo.|**Utilizar existente**. Utiliza la tabla de reescritura existente. Es el valor predeterminado.<br /><br /> **Crear**. Crea una tabla de reescritura y provoca el error del proceso si ya existe una.<br /><br /> **Crear siempre**. Crea una tabla de reescritura, incluso si ya existe una. La tabla existente se elimina y se reemplaza.|  
|**Procesar objetos afectados**|Controla el ámbito del objeto del trabajo de procesamiento. Un objeto afectado se define por la dependencia del objeto. Por ejemplo, las particiones dependen de las dimensiones que determinan la agregación, pero las dimensiones no dependen de las particiones. **False** es la configuración predeterminada.|**False**. El trabajo procesa los objetos con un nombre explícito en el trabajo y todos los objetos dependientes. Por ejemplo, si el trabajo de procesamiento contiene únicamente dimensiones, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] procesa solamente dichos objetos identificados explícitamente en el trabajo. Si el trabajo de procesamiento contiene particiones, el procesamiento de particiones invoca automáticamente el procesamiento de las dimensiones afectadas.<br /><br /> **True**. El trabajo procesa los objetos con nombre explícito en el trabajo, todos los objetos dependientes y todos los objetos afectados por los objetos que se están procesando sin cambiar el estado de los objetos afectados. Por ejemplo, si el trabajo de procesamiento contiene únicamente dimensiones, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] también procesa todas las particiones afectadas por el procesamiento de dimensiones para las particiones que actualmente están en estado procesado. No se procesan las particiones afectadas que actualmente están en estado sin procesar. Sin embargo, dado que las particiones dependen de las dimensiones, si el trabajo de procesamiento contiene únicamente particiones, el procesamiento de particiones invoca automáticamente el procesamiento de las dimensiones afectadas, incluso cuando la dimensión está actualmente en estado sin procesar.|  
|**Errores de clave de dimensión**|Determina la acción realizada por [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] cuando se producen errores durante el procesamiento. Al activar **Usar la configuración de error personalizada**, puede seleccionar valores para las siguientes acciones para controlar el comportamiento del control de errores.<br /><br /> Al activar Utilizar la configuración de error predeterminada, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] utiliza la configuración de error que se establece para cada objeto que se está procesando. Si se establece un objeto para utilizar los valores de configuración predeterminados, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] utiliza la configuración predeterminada enumerada para cada opción.||  
||**Acción del error de clave**. Si aún no existe ningún valor de clave en un registro, se selecciona una de estas acciones:|**Convertir en desconocido**. La clave se interpreta como un miembro desconocido. Esta es la configuración predeterminada.<br /><br /> **Descartar registro**. Se descarta el registro.|  
||**Límite de errores de procesamiento**. Controla la cantidad de errores procesados seleccionando una de estas opciones:|**Omitir recuento de errores**. Permite que continúe el procesamiento, independientemente de la cantidad de errores.<br /><br /> **Detenerse ante errores**. Con esta opción, el usuario controla dos configuraciones adicionales. **Número de errores** permite limitar el procesamiento a la aparición de un número específico de errores. **Acción ante el error** permite determinar la acción cuando se alcanza el **Número de errores** . Puede seleccionar **Detener el procesamiento**, que hace que se detenga el trabajo de procesamiento y se reviertan los cambios, o bien **Detener el registro**, que permite que continúe el procesamiento sin registrar errores. **Detenerse ante errores** es la configuración predeterminada con la opción **Número de errores** establecida como **0** y la opción **Acción ante el error** establecida como **Detener el procesamiento**.|  
||Las siguientes condiciones de error. Puede establecer las siguientes opciones para controlar el comportamiento de control de errores específico:<br /><br /> Al seleccionar **Utilizar la configuración de error predeterminada**, Analysis Services utiliza la configuración de error que se establece para cada objeto que se está procesando. Si se establece un objeto para utilizar los valores de configuración predeterminados, Analysis Services utiliza la configuración predeterminada indicada para cada opción.|**Clave no encontrada**. Se produce cuando existe un valor de clave en una partición, pero no existe en la dimensión correspondiente. La configuración predeterminada es **Informar y continuar**. Otras configuraciones son **Omitir error** e **Informar y detenerse**.<br /><br /> **Clave duplicada**. Se produce cuando existe más de un valor de clave en una dimensión. La configuración predeterminada es **Omitir error**. Otras configuraciones son **Informar y continuar** e **Informar y detenerse**.<br /><br /> **Clave NULL convertida en desconocida**. Se produce cuando un valor de clave es nulo y la **Acción del error de clave** se establece en **Convertir en desconocido**. La configuración predeterminada es **Omitir error**. Otras configuraciones son **Informar y continuar** e **Informar y detenerse**.<br /><br /> **Clave NULL no permitida**. Se produce cuando **Acción del error de clave** se establece en **Descartar registro**. La configuración predeterminada es **Informar y continuar**. Otras configuraciones son **Omitir error** e **Informar y detenerse**.|  
  
## <a name="see-also"></a>Vea también  
 [Procesar un modelo multidimensional &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)  
  
  
