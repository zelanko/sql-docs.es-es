---
title: Realizar operaciones por lotes (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
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
manager: craigg
ms.openlocfilehash: 44ffc8084af6917a8df84c5a204df96112441723
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/26/2018
ms.locfileid: "50148330"
---
# <a name="performing-batch-operations-xmla"></a>Realizar operaciones por lotes (XMLA)
  Puede usar el [Batch](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/batch-element-xmla) comando XML for Analysis (XMLA) para ejecutar varios comandos XMLA con un único XMLA [Execute](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute) método. Puede ejecutar varios comandos incluidos en el comando `Batch`, ya sea como transacción única o en transacciones individuales para cada comando, en serie o en paralelo. También puede especificar los enlaces fuera de línea y otras propiedades en el `Batch` comando para procesar varios [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] objetos.  
  
## <a name="running-transactional-and-nontransactional-batch-commands"></a>Ejecutar comandos Batch transaccionales y no transaccionales  
 El comando `Batch` ejecuta los comandos de una de las dos maneras siguientes:  
  
 **Transaccional**  
 Si el `Transaction` atributo de la `Batch` comando se establece en true, el `Batch` comando ejecuta todos los comandos contenidos por el `Batch` comando en una sola transacción, un *transaccional* por lotes.  
  
 Si se produce un error en cualquier comando en un lote transaccional, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] revierte cualquier comando el `Batch` comando ejecutado antes del comando que no se pudo y la `Batch` comando finaliza inmediatamente. Los comandos contenidos en `Batch` que no se hayan ejecutado aún, no se ejecutan. Una vez finalizado el comando `Batch`, dicho comando `Batch` informa de los errores que se han producido en el comando que no se pudo ejecutar.  
  
 **No transaccional**  
 Si el `Transaction` atributo está establecido en false, el `Batch` comando ejecuta cada comando incluido en el `Batch` comando en una transacción independiente: un *no transaccionales* por lotes. Si se produce un error de cualquiera de los comandos de un lote no transaccional, el comando `Batch` sigue ejecutando los comandos posteriores a aquel que produjo el error. Después de que el comando `Batch` intente ejecutar todos los comandos contenidos en `Batch`, dicho comando `Batch` informa de los errores que se han producido.  
  
 Todos los resultados devueltos por los comandos contenidos en un comando `Batch` se devuelven en el mismo orden en el que éstos están incluidos en el comando `Batch`. Los resultados devueltos por un comando `Batch` varían en función de que el comando `Batch` sea transaccional o no transaccional.  
  
> [!NOTE]  
>  Si un `Batch` comando contiene un comando que no devuelve resultados, como el [bloqueo](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/lock-element-xmla) comando y que comando se ejecuta correctamente, el `Batch` comando devuelve un valor vacío [raíz](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/root-element-xmla) elemento dentro del elemento de resultados. El elemento `root` vacío se asegura de que cada uno de los comandos incluidos en un comando `Batch` pueda coincidir con el elemento `root` adecuado para los resultados de ese comando.  
  
### <a name="returning-results-from-transactional-batch-results"></a>Devolver resultados de lotes transaccionales  
 Los resultados de los comandos ejecutados en un lote transaccional no se devuelven hasta que no se haya completado todo el comando `Batch`. No se devuelven resultados después de ejecutarse cada comando, ya que si se produce un error en cualquiera de los comandos de un lote transaccional, se revertiría el comando `Batch` completo y todos los comandos incluidos en éste. Si todos los comandos de inicio y ejecuta correctamente, el [devolver](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/return-element-xmla) elemento de la [ExecuteResponse](https://docs.microsoft.com/bi-reference/xmla/xml-elements-objects-executeresponse) elemento devuelto por la `Execute` método para el `Batch` comando contiene un [resultados](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/results-element-xmla) elemento, que a su vez contiene uno `root` (elemento) para cada comando ejecutado correctamente contenido en el `Batch` comando. Si cualquiera de los comandos incluidos en el comando `Batch` no se puede iniciar o completar, el método `Execute` devuelve un error de SOAP para el comando `Batch` que contiene el error del comando que no se ejecutó correctamente.  
  
### <a name="returning-results-from-nontransactional-batch-results"></a>Devolver resultados de lotes no transaccionales  
 Los resultados de los comandos que se ejecutan en un lote no transaccional se devuelven en el orden en el que dichos comandos están incluidos dentro del comando `Batch` y según los devuelve cada comando. Si ninguno de los comandos contenidos en el comando `Batch` se puede iniciar correctamente, el método `Execute` devuelve un error de SOAP que contiene un error para el comando `Batch`. Si al menos uno de los comandos se inicia correctamente, el elemento `return` del elemento `ExecuteResponse` devuelto por el método `Execute` para el comando `Batch` contiene un elemento `results` que, a su vez, contiene un elemento `root` por cada comando incluido en el comando `Batch`. Si uno o más comandos en un lote no transaccional no se puede iniciar o completar, el `root` (elemento) para ese comando con errores contiene un [error](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/error-element-xmla) elemento que describe el error.  
  
> [!NOTE]  
>  Siempre que se pueda iniciar al menos uno de los comandos de un lote no transaccional, se considera que dicho lote se ha ejecutado correctamente, incluso aunque cada comando incluido en el lote no transaccional devuelva un error en los resultados del comando `Batch`.  
  
## <a name="using-serial-and-parallel-execution"></a>Utilizar la ejecución en serie y en paralelo  
 Puede utilizar el comando `Batch` para ejecutar los comandos incluidos en serie o en paralelo. Cuando los comandos se ejecutan en serie, el comando siguiente incluido en el comando `Batch` no se puede iniciar hasta que no se complete el comando actualmente en ejecución en el comando `Batch`. Cuando los comandos se ejecutan en paralelo, el comando `Batch` puede ejecutar varios comandos simultáneamente.  
  
 Para ejecutar comandos en paralelo, agregue los comandos para ejecutarse en paralelo a la [paralelo](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/parallel-element-xmla) propiedad de la `Batch` comando. Actualmente, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] puede ejecutar solo contiguos y secuenciales [proceso](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/process-element-xmla) comandos en paralelo. Cualquier otro comando XMLA, como [crear](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/create-element-xmla) o [Alter](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/alter-element-xmla), que se incluye en el `Parallel` propiedad se ejecuta en serie.  
  
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
  
-   Comando 2 se ejecuta en serie una vez completado el comando 1.  
  
-   3 de comando se ejecuta en serie una vez completado el comando 2.  
  
-   Una vez completado el comando 3, ejecute los comandos 4 y 5 en paralelo. Aunque el comando 6 también es un comando `Process`, éste no se puede ejecutar en paralelo con los comandos 4 y 5 porque la propiedad `maxParallel` se ha establecido en 2.  
  
-   El comando 6 se ejecuta en serie una vez completados los comandos 4 y 5.  
  
-   El comando 7 se ejecuta en serie una vez completado el comando 6.  
  
-   Los comandos 8 y 9 se ejecutan en paralelo una vez completado el comando 7.  
  
## <a name="using-the-batch-command-to-process-objects"></a>Utilizar el comando Batch para procesar objetos  
 El comando `Batch` contiene varias propiedades y atributos opcionales incluidos específicamente para admitir el procesamiento de varios proyectos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]:  
  
-   El atributo `ProcessAffectedObjects` del comando `Batch` indica si la instancia también debe procesar cualquier objeto que sea necesario volver a procesar como resultado de la inclusión de un comando `Process` en el comando `Batch` que procesa un objeto especificado.  
  
-   El [enlaces](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/bindings-element-xmla) propiedad contiene una colección de enlaces fuera de línea utilizado por todos los `Process` comandos en el `Batch` comando.  
  
-   El [DataSource](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/source-element-xmla) propiedad contiene un enlace fuera de línea para un origen de datos utilizado por todos los `Process` comandos en el `Batch` comando.  
  
-   El [DataSourceView](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/datasourceview-element-xmla) propiedad contiene un enlace fuera de línea para una vista del origen de datos utilizado por todos los `Process` comandos en el `Batch` comando.  
  
-   El [ErrorConfiguration](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/errorconfiguration-element-xmla) propiedad especifica la manera en que el `Batch` comando controla los errores detectados por todos los `Process` los comandos contenidos en el `Batch` comando.  
  
    > [!IMPORTANT]  
    >  Un comando `Process` no puede incluir las propiedades `Bindings`, `DataSource`, `DataSourceView` o `ErrorConfiguration` si dicho comando `Process` está incluido en un comando `Batch`. Si debe especificar estas propiedades para un comando `Process`, proporcione la información necesaria en las propiedades correspondientes del comando `Batch` que contiene el comando `Process`.  
  
## <a name="see-also"></a>Vea también  
 [Elemento de lote &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/batch-element-xmla)   
 [Procesar el elemento &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/process-element-xmla)   
 [Procesamiento de objetos de modelo multidimensional](../multidimensional-models/processing-a-multidimensional-model-analysis-services.md)   
 [Desarrollo con XMLA en Analysis Services](developing-with-xmla-in-analysis-services.md)  
  
  
