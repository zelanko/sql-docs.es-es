---
title: Realizar operaciones por lotes (XMLA) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6c451d13016915c9218efb2963429f8f5a7709e2
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52544228"
---
# <a name="performing-batch-operations-xmla"></a>Realizar operaciones por lotes (XMLA)
  Puede usar el [Batch](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/batch-element-xmla) comando XML for Analysis (XMLA) para ejecutar varios comandos XMLA con un único XMLA [Execute](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute) método. Puede ejecutar varios comandos incluidos en el **Batch** comando como una única transacción o en transacciones individuales para cada comando, en serie o en paralelo. También puede especificar los enlaces fuera de línea y otras propiedades en el **Batch** comando para procesar varios [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] objetos.  
  
## <a name="running-transactional-and-nontransactional-batch-commands"></a>Ejecutar comandos Batch transaccionales y no transaccionales  
 El **Batch** comando ejecuta los comandos de dos maneras:  
  
 **Transaccional**  
 Si el **transacciones** atributo de la **Batch** comando se establece en true, el **por lotes** comando ejecuta todos los comandos contenidos por el **Batch** comando en una única transacción, un *transaccional* por lotes.  
  
 Si se produce un error en cualquier comando en un lote transaccional, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] revierte cualquier comando el **Batch** comando ejecutado antes del comando que no se pudo y la **Batch** comando finaliza inmediatamente. Cualquier comando en el **Batch** no se ejecutó el comando que aún no se han ejecutado. Después de la **Batch** comando finaliza, el **Batch** comando informa de los errores producidos durante el comando con errores.  
  
 **No transaccional**  
 Si el **transacciones** atributo está establecido en false, el **Batch** comando ejecuta cada comando incluido en el **Batch** otra transacción, un comando  *no transaccionales* por lotes. Si se produce un error en cualquier comando en un lote no transaccional, el **Batch** comando sigue ejecutando los comandos posteriores que produjo el error. Después de la **Batch** comando intenta ejecutar todos los comandos que el **por lotes** contiene el comando, el **Batch** comando informa de los errores producidos.  
  
 Todos los resultados devueltos por los comandos contenidos en un **Batch** comando se devuelven en el mismo orden en que se encuentran los comandos en el **Batch** comando. Los resultados devueltos por una **Batch** comando varían en función de si el **Batch** comando es transaccional o no transaccional.  
  
> [!NOTE]  
>  Si un **Batch** comando contiene un comando que no devuelve resultados, como el [bloqueo](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/lock-element-xmla) comando y que comando se ejecuta correctamente, el **Batch** comando devuelve un valor vacío [raíz](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/root-element-xmla) dentro del elemento de resultados. Vacío **raíz** elemento garantiza que cada comando incluido en un **Batch** comando coinciden con los valores adecuados **raíz** (elemento) para los resultados de ese comando.  
  
### <a name="returning-results-from-transactional-batch-results"></a>Devolver resultados de lotes transaccionales  
 No se devuelven los resultados de comandos que se ejecutan dentro de un lote transaccional hasta que toda la **Batch** completado el comando. No se devuelven los resultados después de cada comando se ejecuta porque cualquiera de los comandos que se produce un error dentro de un lote transaccional provocaría toda la **Batch** comando y todos los comandos que lo contiene se reviertan. Si todos los comandos de inicio y ejecuta correctamente, el [devolver](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/return-element-xmla) elemento de la [ExecuteResponse](https://docs.microsoft.com/bi-reference/xmla/xml-elements-objects-executeresponse) elemento devuelto por la **Execute** método para el **por lotes**  comando contiene un [resultados](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/results-element-xmla) elemento, que a su vez contiene uno **raíz** (elemento) para cada comando ejecutado correctamente contenido en el **Batch** comando. Si cualquiera de los comandos en el **Batch** comando no se puede iniciar o completar, el **Execute** método devuelve un error de SOAP para el **Batch** comando que contiene el error de la comando con errores.  
  
### <a name="returning-results-from-nontransactional-batch-results"></a>Devolver resultados de lotes no transaccionales  
 Resultados de comandos que se ejecutan dentro de un lote no transaccional se devuelven en el orden en que se encuentran los comandos dentro de la **Batch** comando y que son devueltos por cada comando. Si no hay ningún comando contenido en el **Batch** comando se puede iniciar correctamente, el **Execute** método devuelve un error de SOAP que contiene un error para el **Batch** comando. Si se ha iniciado correctamente al menos un comando, el **devolver** elemento de la **ExecuteResponse** elemento devuelto por la **Execute** método para el **por lotes**  comando contiene un **resultados** elemento, que a su vez contiene uno **raíz** (elemento) para cada comando incluido en el **Batch** comando . Si uno o más comandos en un lote no transaccional no se puede iniciar o completar, el **raíz** (elemento) para ese comando con errores contiene un [error](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/error-element-xmla) elemento que describe el error.  
  
> [!NOTE]  
>  Siempre que se puede iniciar al menos un comando en un lote no transaccional, el lote no transaccional se considera que ha ejecutado correctamente, aunque cada comando incluido en el lote no transaccional devuelva un error en los resultados de la **por lotes**  comando.  
  
## <a name="using-serial-and-parallel-execution"></a>Utilizar la ejecución en serie y en paralelo  
 Puede usar el **Batch** comando para ejecutar incluye comandos en serie o en paralelo. Cuando los comandos se ejecutan en serie, el comando siguiente incluido en el **Batch** comando no se puede iniciar hasta que el comando que se está ejecutando en el **Batch** completado el comando. Cuando los comandos se ejecutan en paralelo, se pueden ejecutar varios comandos simultáneamente mediante el **Batch** comando.  
  
 Para ejecutar comandos en paralelo, agregue los comandos para ejecutarse en paralelo a la [paralelo](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/parallel-element-xmla) propiedad de la **Batch** comando. Actualmente, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] puede ejecutar solo contiguos y secuenciales [proceso](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/process-element-xmla) comandos en paralelo. Cualquier otro comando XMLA, como [crear](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/create-element-xmla) o [Alter](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/alter-element-xmla), que se incluye en el **paralelo** propiedad se ejecuta en serie.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] intenta ejecutar todos los **proceso** comandos incluidos en el **paralelo** propiedad en paralelo, pero no puede garantizar que todo incluido **proceso** comandos se pueden ejecutar en paralelo. La instancia analiza cada **proceso** comando y, si la instancia determina que el comando no se puede ejecutar en paralelo, el **proceso** comando se ejecuta en serie.  
  
> [!NOTE]  
>  Para ejecutar comandos en paralelo, el **transacciones** atributo de la **Batch** comandos deben establecerse en "true" porque [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] admite solo una transacción activa por conexión y no transaccionales lotes que se ejecute cada comando en una transacción independiente. Si incluye el **paralelo** propiedad en un lote no transaccional, que se produce un error.  
  
### <a name="limiting-parallel-execution"></a>Limitar la ejecución en paralelo  
 Un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instancia intenta ejecutar tantos **proceso** comandos en paralelo como sea posible, hasta los límites del equipo en el que se ejecuta la instancia. Puede limitar el número de la que se ejecutan concurrentemente **proceso** comandos estableciendo el **maxParallel** atributo de la **paralelo** propiedad a un valor que indica el número máximo de **proceso** comandos que se pueden ejecutar en paralelo.  
  
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
  
 El **maxParalle**atributo l de este **paralelo** propiedad está establecida en 2. Por lo tanto, la instancia ejecuta la lista de comandos anteriores como se describe en la lista siguiente:  
  
-   Comando 1 se ejecuta en serie porque el comando 1 es un **crear** comando y solo **proceso** comandos se pueden ejecutar en paralelo.  
  
-   Comando 2 se ejecuta en serie una vez completado el comando 1.  
  
-   3 de comando se ejecuta en serie una vez completado el comando 2.  
  
-   Una vez completado el comando 3, ejecute los comandos 4 y 5 en paralelo. Aunque el comando 6 también es un **proceso** comando, el comando 6 no se puede ejecutar en paralelo con los comandos 4 y 5 porque el **maxParallel** propiedad está establecida en 2.  
  
-   El comando 6 se ejecuta en serie una vez completados los comandos 4 y 5.  
  
-   El comando 7 se ejecuta en serie una vez completado el comando 6.  
  
-   Los comandos 8 y 9 se ejecutan en paralelo una vez completado el comando 7.  
  
## <a name="using-the-batch-command-to-process-objects"></a>Utilizar el comando Batch para procesar objetos  
 El **Batch** comando contiene varias propiedades y atributos opcionales incluidos específicamente para admitir procesar varios [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] proyectos:  
  
-   El **ProcessAffectedObjects** atributo de la **Batch** comando indica si la instancia también debe procesar cualquier objeto que requiere volver a procesar como resultado de una **proceso** comando incluido en el **Batch** comando procesa un objeto especificado.  
  
-   El [enlaces](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/bindings-element-xmla) propiedad contiene una colección de enlaces fuera de línea utilizado por todos los **proceso** comandos en el **Batch** comando.  
  
-   El [DataSource](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/datasource-element-xmla) propiedad contiene un enlace fuera de línea para un origen de datos utilizado por todos los **proceso** comandos en el **Batch** comando.  
  
-   El [DataSourceView](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/datasourceview-element-xmla) propiedad contiene un enlace fuera de línea para una vista del origen de datos utilizado por todos los **proceso** comandos en el **Batch** comando.  
  
-   El [ErrorConfiguration](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/errorconfiguration-element-xmla) propiedad especifica la manera en que el **Batch** comando controla los errores detectados por todos los **proceso** los comandos contenidos en el **Batch** comando.  
  
    > [!IMPORTANT]  
    >  Un **proceso** comando no se puede incluir el **enlaces**, **DataSource**, **DataSourceView**, o **ErrorConfiguration**  propiedades, si la **proceso** comandos se encuentra en un **Batch** comando. Si debe especificar estas propiedades para un **proceso** comando, proporcione la información necesaria en las propiedades correspondientes de la **Batch** comando que contiene el **proceso** comando.  
  
## <a name="see-also"></a>Vea también  
 [Elemento de lote &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/batch-element-xmla)   
 [Procesar el elemento &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/process-element-xmla)   
 [Procesar un modelo multidimensional &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)   
 [Desarrollo con XMLA en Analysis Services](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
