---
title: Realización de operaciones por lotes (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
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
author: minewiskan
ms.author: owend
ms.openlocfilehash: 69899077cf534482879accbf10640f6295e3866a
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/09/2020
ms.locfileid: "84544928"
---
# <a name="performing-batch-operations-xmla"></a>Realizar operaciones por lotes (XMLA)
  Puede usar el comando [batch](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/batch-element-xmla) en XML for Analysis (XMLA) para ejecutar varios comandos XMLA con un solo método [Execute](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute) de XMLA. Puede ejecutar varios comandos incluidos en el comando `Batch`, ya sea como transacción única o en transacciones individuales para cada comando, en serie o en paralelo. También puede especificar enlaces fuera de línea y otras propiedades en el `Batch` comando para procesar varios [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] objetos.  
  
## <a name="running-transactional-and-nontransactional-batch-commands"></a>Ejecutar comandos Batch transaccionales y no transaccionales  
 El comando `Batch` ejecuta los comandos de una de las dos maneras siguientes:  
  
 **Transaccional**  
 Si el `Transaction` atributo del `Batch` comando se establece en true, el `Batch` comando ejecuta comandos todos los comandos incluidos `Batch` en el comando en una sola transacción: un lote *transaccional* .  
  
 Si algún comando produce un error en un lote transaccional, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] revierte cualquier comando del `Batch` comando que se ejecutó antes de que se produjeron errores en el comando y que el `Batch` comando finalice inmediatamente. Los comandos contenidos en `Batch` que no se hayan ejecutado aún, no se ejecutan. Una vez finalizado el comando `Batch`, dicho comando `Batch` informa de los errores que se han producido en el comando que no se pudo ejecutar.  
  
 **No transaccional**  
 Si el `Transaction` atributo se establece en false, el `Batch` comando ejecuta cada comando incluido en el `Batch` comando en una transacción independiente: un lote no *transaccional* . Si se produce un error de cualquiera de los comandos de un lote no transaccional, el comando `Batch` sigue ejecutando los comandos posteriores a aquel que produjo el error. Después de que el comando `Batch` intente ejecutar todos los comandos contenidos en `Batch`, dicho comando `Batch` informa de los errores que se han producido.  
  
 Todos los resultados devueltos por los comandos contenidos en un comando `Batch` se devuelven en el mismo orden en el que éstos están incluidos en el comando `Batch`. Los resultados devueltos por un comando `Batch` varían en función de que el comando `Batch` sea transaccional o no transaccional.  
  
> [!NOTE]  
>  Si un `Batch` comando contiene un comando que no devuelve resultados, como el comando [Lock](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/lock-element-xmla) , y ese comando se ejecuta correctamente, el `Batch` comando devuelve un elemento [raíz](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/root-element-xmla) vacío dentro del elemento Results. El elemento `root` vacío se asegura de que cada uno de los comandos incluidos en un comando `Batch` pueda coincidir con el elemento `root` adecuado para los resultados de ese comando.  
  
### <a name="returning-results-from-transactional-batch-results"></a>Devolver resultados de lotes transaccionales  
 Los resultados de los comandos ejecutados en un lote transaccional no se devuelven hasta que no se haya completado todo el comando `Batch`. No se devuelven resultados después de ejecutarse cada comando, ya que si se produce un error en cualquiera de los comandos de un lote transaccional, se revertiría el comando `Batch` completo y todos los comandos incluidos en éste. Si todos los comandos se inician y se ejecutan correctamente, el elemento [Return](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/return-element-xmla) del elemento [ExecuteResponse](https://docs.microsoft.com/bi-reference/xmla/xml-elements-objects-executeresponse) devuelto por el `Execute` método para el `Batch` comando contiene un elemento [Results](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/results-element-xmla) , que a su vez contiene un `root` elemento para cada comando ejecutado correctamente incluido en el `Batch` comando. Si cualquiera de los comandos incluidos en el comando `Batch` no se puede iniciar o completar, el método `Execute` devuelve un error de SOAP para el comando `Batch` que contiene el error del comando que no se ejecutó correctamente.  
  
### <a name="returning-results-from-nontransactional-batch-results"></a>Devolver resultados de lotes no transaccionales  
 Los resultados de los comandos que se ejecutan en un lote no transaccional se devuelven en el orden en el que dichos comandos están incluidos dentro del comando `Batch` y según los devuelve cada comando. Si ninguno de los comandos contenidos en el comando `Batch` se puede iniciar correctamente, el método `Execute` devuelve un error de SOAP que contiene un error para el comando `Batch`. Si al menos uno de los comandos se inicia correctamente, el elemento `return` del elemento `ExecuteResponse` devuelto por el método `Execute` para el comando `Batch` contiene un elemento `results` que, a su vez, contiene un elemento `root` por cada comando incluido en el comando `Batch`. Si uno o varios comandos de un lote no transaccional no se pueden iniciar o no se completan correctamente, el `root` elemento de ese comando con error contiene un elemento de [error](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/error-element-xmla) que describe el error.  
  
> [!NOTE]  
>  Siempre que se pueda iniciar al menos uno de los comandos de un lote no transaccional, se considera que dicho lote se ha ejecutado correctamente, incluso aunque cada comando incluido en el lote no transaccional devuelva un error en los resultados del comando `Batch`.  
  
## <a name="using-serial-and-parallel-execution"></a>Utilizar la ejecución en serie y en paralelo  
 Puede utilizar el comando `Batch` para ejecutar los comandos incluidos en serie o en paralelo. Cuando los comandos se ejecutan en serie, el comando siguiente incluido en el comando `Batch` no se puede iniciar hasta que no se complete el comando actualmente en ejecución en el comando `Batch`. Cuando los comandos se ejecutan en paralelo, el comando `Batch` puede ejecutar varios comandos simultáneamente.  
  
 Para ejecutar comandos en paralelo, agregue los comandos que se ejecutarán en paralelo a la propiedad [Parallel](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/parallel-element-xmla) del `Batch` comando. Actualmente, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] solo puede ejecutar comandos de [proceso](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/process-element-xmla) consecutivos contiguos en paralelo. Cualquier otro comando XMLA, como [Create](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/create-element-xmla) o [ALTER](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/alter-element-xmla), incluido en la `Parallel` propiedad se ejecuta en serie.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] intenta ejecutar todos los comandos `Process` incluidos en la propiedad `Parallel` en paralelo, pero no puede garantizar que todos los comandos `Process` incluidos puedan ejecutarse en paralelo. La instancia analiza cada uno de los comandos `Process` y, si ésta determina que el comando no se puede ejecutar en paralelo, el comando `Process` se ejecuta en serie.  
  
> [!NOTE]  
>  Para ejecutar los comandos en paralelo, el atributo `Transaction` del comando `Batch` debe establecerse en true, ya que [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] solo admite una transacción activa por conexión y los lotes no transaccionales ejecutan cada uno de los comandos en una transacción independiente. Si incluye la propiedad `Parallel` en un lote no transaccional, se produce un error.  
  
### <a name="limiting-parallel-execution"></a>Limitar la ejecución en paralelo  
 Una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] intenta ejecutar en paralelo tantos comandos `Process` como sea posible, hasta alcanzar los límites del equipo en el que se ejecuta la instancia. Para limitar el número de comandos `Process` que se ejecutan simultáneamente, establezca el atributo `maxParallel` de la propiedad `Parallel` en un valor que indique el número máximo de comandos `Process` que pueden ejecutarse en paralelo.  
  
 Por ejemplo, una propiedad `Parallel` contiene los siguientes comandos en el orden que se muestra:  
  
1.  `Create`  
  
2.  `Process`  
  
3.  `Alter`  
  
4.  `Process`  
  
5.  `Process`  
  
6.  `Process`  
  
7.  `Delete`  
  
8.  `Process`  
  
9. `Process`  
  
 El atributo `maxParalle` de esta propiedad `Parallel` se ha establecido en 2. Por lo tanto, la instancia ejecuta la lista de comandos anteriores como se describe en la lista siguiente:  
  
-   El comando 1 se ejecuta en serie porque es un comando `Create` y solamente se pueden ejecutar en paralelo los comandos `Process`.  
  
-   El comando 2 se ejecuta en serie una vez completado el comando 1.  
  
-   El comando 3 se ejecuta en serie una vez completado el comando 2.  
  
-   Los comandos 4 y 5 se ejecutan en paralelo después de completar el comando 3. Aunque el comando 6 también es un comando `Process`, éste no se puede ejecutar en paralelo con los comandos 4 y 5 porque la propiedad `maxParallel` se ha establecido en 2.  
  
-   El comando 6 se ejecuta en serie una vez completados los comandos 4 y 5.  
  
-   El comando 7 se ejecuta en serie una vez completado el comando 6.  
  
-   Los comandos 8 y 9 se ejecutan en paralelo una vez completado el comando 7.  
  
## <a name="using-the-batch-command-to-process-objects"></a>Utilizar el comando Batch para procesar objetos  
 El comando `Batch` contiene varias propiedades y atributos opcionales incluidos específicamente para admitir el procesamiento de varios proyectos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]:  
  
-   El atributo `ProcessAffectedObjects` del comando `Batch` indica si la instancia también debe procesar cualquier objeto que sea necesario volver a procesar como resultado de la inclusión de un comando `Process` en el comando `Batch` que procesa un objeto especificado.  
  
-   La propiedad [bindings](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/bindings-element-xmla) contiene una colección de enlaces fuera de línea utilizados por todos los `Process` comandos del `Batch` comando.  
  
-   La propiedad [DataSource](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/source-element-xmla) contiene un enlace fuera de línea para un origen de datos utilizado por todos los comandos del `Process` `Batch` comando.  
  
-   La propiedad [DataSourceView](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/datasourceview-element-xmla) contiene un enlace fuera de línea para una vista del origen de datos utilizada por todos los `Process` comandos del `Batch` comando.  
  
-   La propiedad [ErrorConfiguration](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/errorconfiguration-element-xmla) especifica la forma en que el `Batch` comando controla los errores detectados por todos los `Process` comandos contenidos en el `Batch` comando.  
  
    > [!IMPORTANT]  
    >  Un comando `Process` no puede incluir las propiedades `Bindings`, `DataSource`, `DataSourceView` o `ErrorConfiguration` si dicho comando `Process` está incluido en un comando `Batch`. Si debe especificar estas propiedades para un comando `Process`, proporcione la información necesaria en las propiedades correspondientes del comando `Batch` que contiene el comando `Process`.  
  
## <a name="see-also"></a>Consulte también  
 [Elemento batch &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/batch-element-xmla)   
 [Elemento Process &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/process-element-xmla)   
 [Procesamiento de objetos del modelo multidimensional](../multidimensional-models/processing-a-multidimensional-model-analysis-services.md)   
 [Desarrollar con XMLA en Analysis Services](developing-with-xmla-in-analysis-services.md)  
  
  
