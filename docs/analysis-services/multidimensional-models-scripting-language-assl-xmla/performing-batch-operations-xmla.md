---
title: Realizar operaciones por lotes (XMLA) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- multiple projects
- XML for Analysis, batches
- parallel batch execution [XMLA]
- transactional batches
- serial batch execution [XMLA]
- XMLA, batches
- batches [XML for Analysis]
- nontransactional batches
ms.assetid: 731c70e5-ed51-46de-bb69-cbf5aea18dda
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3e2673091cfba456834da77049036591e4591891
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="performing-batch-operations-xmla"></a>Realizar operaciones por lotes (XMLA)
  Puede usar el [lote](../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md) comando XML for Analysis (XMLA) para ejecutar varios comandos XMLA con un único XMLA [Execute](../../analysis-services/xmla/xml-elements-methods-execute.md) método. Puede ejecutar varios comandos incluidos en el **lote** comando como una única transacción o en transacciones individuales para cada comando, en serie o en paralelo. También puede especificar enlaces fuera de línea y otras propiedades en la **lote** comando para procesar varios [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] objetos.  
  
## <a name="running-transactional-and-nontransactional-batch-commands"></a>Ejecutar comandos Batch transaccionales y no transaccionales  
 El **lote** comando ejecuta comandos en una de dos maneras:  
  
 **Transaccional**  
 Si el **transacciones** atributo de la **lote** comando se establece en true, el **lote** comando ejecuta todos los comandos contenidos por el **lote** comando en una sola transacción, un *transaccional* por lotes.  
  
 Si se produce un error en cualquier comando en un lote transaccional, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] revierte cualquier comando la **lote** comando ejecutado antes del comando que no se pudo y la **lote** comando finaliza inmediatamente. Los comandos en el **lote** no se ejecutó el comando que no se han ejecutado todavía. Después de la **lote** comando finalice, el **lote** comando informa de los errores que se produjeron en el comando con errores.  
  
 **No transaccional**  
 Si el **transacciones** atributo está establecido en false, el **lote** comando ejecuta cada comando incluido en el **lote** comando en una transacción independiente: un  *no transaccionales* por lotes. Si se produce un error en cualquier comando en un lote no transaccional, el **lote** comando continúa ejecutar comandos después del comando que produjeron errores. Después de la **lote** comando intenta ejecutar todos los comandos que el **lote** contiene el comando, el **lote** comando informa de los errores producidos.  
  
 Todos los resultados devueltos por los comandos contenidos en un **lote** comandos se devuelven en el mismo orden en que se encuentran los comandos en el **lote** comando. Los resultados devueltos por una **lote** comando varían en función de si la **lote** comando es transaccional o no transaccional.  
  
> [!NOTE]  
>  Si un **lote** comando contiene un comando que no devuelve resultados, como el [bloqueo](../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md) comando y que comando se ejecuta correctamente, el **lote** comando devuelve una instancia vacía [raíz](../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md) dentro del elemento de resultados. Vacío **raíz** elemento garantiza que cada comando incluido en un **lote** comando puede coincidir con la correspondiente **raíz** , elemento de resultados de ese comando.  
  
### <a name="returning-results-from-transactional-batch-results"></a>Devolver resultados de lotes transaccionales  
 No se devuelven los resultados de los comandos que se ejecutan dentro de un lote transaccional hasta que toda la matriz **lote** completado el comando. No se devuelven los resultados después de cada comando se ejecuta porque cualquiera de los comandos que se produce un error dentro de un lote transaccional provocaría que toda la matriz **lote** comando y todos los comandos se revierta. Si todos los comandos se inicia y se ejecuta correctamente, el [devolver](../../analysis-services/xmla/xml-elements-properties/return-element-xmla.md) elemento de la [ExecuteResponse](../../analysis-services/xmla/xml-elements-objects-executeresponse.md) elemento devuelto por la **Execute** método para el **por lotes**  comando contiene un [resultados](../../analysis-services/xmla/xml-elements-properties/results-element-xmla.md) elemento, que a su vez contiene uno **raíz** (elemento) para cada comando ejecutado correctamente contenido en el **lote** comando. Si cualquiera de los comandos en el **lote** comando no se puede iniciar o completar, el **Execute** método devuelve un error de SOAP para el **lote** comando que contiene el error de la comando que no se pudo.  
  
### <a name="returning-results-from-nontransactional-batch-results"></a>Devolver resultados de lotes no transaccionales  
 Resultados de los comandos que se ejecutan dentro de un lote no transaccional se devuelven en el orden en el que los comandos están incluidos dentro de la **lote** comando y que son devueltos por cada comando. Si no hay ningún comando contenido en el **lote** comando se puede iniciar correctamente, el **Execute** método devuelve un error de SOAP que contiene un error para la **lote** comando. Si se ha iniciado correctamente al menos un comando, el **devolver** elemento de la **ExecuteResponse** elemento devuelto por la **Execute** método para el **por lotes**  comando contiene un **resultados** elemento, que a su vez contiene uno **raíz** (elemento) para cada comando incluido en el **lote** comando . Si uno o más comandos en un lote no transaccional no se puede iniciar o completar, el **raíz** (elemento) para dicho comando con errores contiene una [error](../../analysis-services/xmla/xml-elements-properties/error-element-xmla.md) elemento que describe el error.  
  
> [!NOTE]  
>  Siempre que se puede iniciar al menos un comando en un lote no transaccional, el lote no transaccional se considera que ha ejecutado correctamente, aunque cada comando incluido en el lote no transaccional devuelva un error en los resultados de la **por lotes**  comando.  
  
## <a name="using-serial-and-parallel-execution"></a>Utilizar la ejecución en serie y en paralelo  
 Puede usar el **lote** comando para ejecutar incluye comandos en serie o en paralelo. Cuando los comandos se ejecutan en serie, el comando siguiente incluido en el **lote** comando no se puede iniciar hasta que el comando se está ejecutando en el **lote** completado el comando. Cuando los comandos se ejecutan en paralelo, se pueden ejecutar varios comandos simultáneamente mediante la **lote** comando.  
  
 Para ejecutar comandos en paralelo, agregue los comandos que se ejecutarán en paralelo a la [paralelo](../../analysis-services/xmla/xml-elements-properties/parallel-element-xmla.md) propiedad de la **lote** comando. Actualmente, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] puede ejecutar solo contiguos y secuenciales [proceso](../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md) comandos en paralelo. Cualquier otro comando XMLA, como [crear](../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md) o [Alter](../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md), incluido en el **paralelo** propiedad se ejecuta en serie.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]intenta ejecutar todos los **proceso** comandos incluidos en el **paralelo** propiedad en paralelo, pero no puede garantizar que todo incluido **proceso** comandos se pueden ejecutar en paralelo. La instancia analiza cada uno **proceso** comando y, si la instancia determina que el comando no se puede ejecutar en paralelo, la **proceso** comando se ejecuta en serie.  
  
> [!NOTE]  
>  Para ejecutar comandos en paralelo, la **transacciones** atributo de la **lote** comando debe establecerse en true porque [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] admite solo una transacción activa por conexión y no transaccionales lotes que se ejecute cada comando en una transacción independiente. Si incluye el **paralelo** propiedad en un lote no transaccional, que se produce un error.  
  
### <a name="limiting-parallel-execution"></a>Limitar la ejecución en paralelo  
 Un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instancia intenta ejecutar tantos **proceso** comandos en paralelo como sea posible, hasta los límites del equipo en el que se ejecuta la instancia. Puede limitar el número de que se ejecutan concurrentemente **proceso** comandos estableciendo la **maxParallel** atributo de la **paralelo** propiedad a un valor que indica el número máximo de **proceso** comandos que se pueden ejecutar en paralelo.  
  
 Por ejemplo, un **paralelo** propiedad contiene los siguientes comandos en el orden indicado:  
  
1.  **Crear**  
  
2.  **Procesar**  
  
3.  **Alter**  
  
4.  **Procesar**  
  
5.  **Procesar**  
  
6.  **Procesar**  
  
7.  **Eliminar**  
  
8.  **Procesar**  
  
9. **Procesar**  
  
 El **maxParalle**de este atributo **paralelo** propiedad está establecida en 2. Por lo tanto, la instancia ejecuta la lista de comandos anteriores como se describe en la lista siguiente:  
  
-   Comando 1 se ejecuta en serie porque comando 1 es un **crear** comando y solo **proceso** comandos se pueden ejecutar en paralelo.  
  
-   Comando 2 se ejecuta en serie una vez completado el comando 1.  
  
-   Comando 3 se ejecuta en serie una vez completado el comando 2.  
  
-   Comandos 4 y 5 se ejecutan en paralelo una vez completado el comando 3. Aunque el comando 6 también es un **proceso** comando, el comando 6 no se puede ejecutar en paralelo con los comandos 4 y 5 porque el **maxParallel** propiedad está establecida en 2.  
  
-   El comando 6 se ejecuta en serie una vez completados los comandos 4 y 5.  
  
-   El comando 7 se ejecuta en serie una vez completado el comando 6.  
  
-   Los comandos 8 y 9 se ejecutan en paralelo una vez completado el comando 7.  
  
## <a name="using-the-batch-command-to-process-objects"></a>Utilizar el comando Batch para procesar objetos  
 El **lote** comando contiene varias propiedades y atributos opcionales incluidos específicamente para admitir el procesamiento de varios [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] proyectos:  
  
-   El **ProcessAffectedObjects** atributo de la **lote** comando indica si la instancia también debe procesar cualquier objeto que requiere volver a procesar como resultado de una **proceso** comando incluido en el **lote** comando procesa un objeto especificado.  
  
-   El [enlaces](../../analysis-services/xmla/xml-elements-properties/bindings-element-xmla.md) propiedad contiene una colección de enlaces fuera de línea utilizado por todos los **proceso** comandos en el **lote** comando.  
  
-   El [DataSource](../../analysis-services/xmla/xml-elements-properties/datasource-element-xmla.md) propiedad contiene un enlace fuera de línea para un origen de datos utilizado por todos los **proceso** comandos en el **lote** comando.  
  
-   El [DataSourceView](../../analysis-services/xmla/xml-elements-properties/datasourceview-element-xmla.md) propiedad contiene un enlace fuera de línea para una vista del origen de datos utilizado por todos los **proceso** comandos en el **lote** comando.  
  
-   El [ErrorConfiguration](../../analysis-services/xmla/xml-elements-properties/errorconfiguration-element-xmla.md) propiedad especifica la forma en que la **lote** comando controla los errores detectados por todos los **proceso** comandos contenidos en el **Lote** comando.  
  
    > [!IMPORTANT]  
    >  A **proceso** comando no se puede incluir la **enlaces**, **DataSource**, **DataSourceView**, o **ErrorConfiguration**  propiedades, si la **proceso** comandos se encuentra en un **lote** comando. Si debe especificar estas propiedades para un **proceso** comando, proporcione la información necesaria en las propiedades correspondientes de la **lote** comando que contiene el **deproceso** comando.  
  
## <a name="see-also"></a>Vea también  
 [Elemento de lote &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)   
 [Process, elemento &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)   
 [Procesar un modelo multidimensional &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)   
 [Desarrollar con XMLA en Analysis Services](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  

