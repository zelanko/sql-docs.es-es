---
title: Escenarios de implementación de DirectQuery (SSAS Tabular) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 2aaf5cb8-294b-4031-94b3-fe605d7fc4c7
caps.latest.revision: 17
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 89454dfd53b641401352928ecf8e08b4b23e784c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37268021"
---
# <a name="directquery-deployment-scenarios-ssas-tabular"></a>Escenarios de implementación de DirectQuery (SSAS tabular)
  Este tema proporciona un tutorial del proceso de diseño e implementación para los modelos de DirectQuery. Puede configurar DirectQuery para utilizar solo datos relacionales (solo DirectQuery), o puede configurar el modelo para cambiar entre usar solo datos en caché o solo datos relacionales (modo híbrido). En este tema se describe el proceso de implementación para ambos modos, y describe diferencias posibles en los resultados de la consulta dependiendo del modo y configuración de seguridad.  
  
 [Diseño y los pasos de implementación](#bkmk_DQProcedure)  
  
 [Comparación de las configuraciones de DirectQuery](#bkmk_Configurations)  
  
##  <a name="bkmk_DQProcedure"></a> Diseño y los pasos de implementación  
 **Paso 1. Crear la solución**  
  
 Independientemente del modo que utilizará, debe revisar la información que describe las limitaciones en los datos que se pueden utilizar en los modelos de DirectQuery. Por ejemplo, todos los datos usados en el modelo y los informes deben proceder de una sola base de datos de SQL Server. Para más información, vea [Modo DirectQuery &#40;SSAS tabular&#41;](tabular-models/directquery-mode-ssas-tabular.md).  
  
 Además, revise las limitaciones de las medidas y columnas calculadas, y determine si las fórmulas que piensa utilizar son compatibles con el modo de DirectQuery. Podría necesitar quitar o modificar los siguientes elementos:  
  
-   Las columnas calculadas no se admiten.  
  
-   Los datos copiados-pegados no se pueden utilizar. Si importa un modelo de PowerPivot para iniciar la solución, asegúrese de eliminar las tablas vinculadas antes de importar la solución, ya que estos datos no se pueden eliminar y bloquearán la validación de DirectQuery.  
  
 **Paso 2. Habilitar el modo DirectQuery en el Diseñador de modelos**  
  
 De forma predeterminada, DirectQuery está deshabilitado. Por tanto, debe configurar el entorno de diseño para admitir el modo de DirectQuery.  
  
 Haga clic en el **Model.bim** nodo en el Explorador de soluciones y establezca la propiedad **Directquerymode**a `On`.  
  
 Puede activar DirectQuery en cualquier momento; sin embargo, para asegurarse de que no crea columnas o fórmulas incompatibles con el modo DirectQuery, se recomienda habilitar el modo DirectQuery desde el principio.  
  
 Inicialmente, incluso los modelos de DirectQuery se crean siempre en memoria. El modo de consulta predeterminado para la base de datos del área de trabajo también se establece en **DirectQuery con In-Memory**. Este modo de funcionamiento híbrido permite utilizar la memoria caché de los datos importados para mejorar el rendimiento durante el proceso de diseño de modelos mientras se valida el modelo con los requisitos de DirectQuery.  
  
 **Paso 3. Resolver errores de validación**  
  
 Si obtiene errores de validación al activar DirectQuery, o al agregar nuevos datos o nuevas fórmulas, abra la **Lista de errores**de Visual Studio y tome las medidas necesarias.  
  
-   Cambie los valores de las propiedades requeridos para el modo DirectQuery, tal como se describe en los mensajes de error.  
  
-   Quite las columnas calculadas. Si necesita una columna calculada para una medida determinada, siempre puede crear la columna mediante el uso de la [Diseñador de consultas relacionales &#40;SSAS&#41; ](relational-query-designer-ssas.md) proporcionada en el Asistente de importación de tablas.  
  
-   Modifique o quite las fórmulas incompatibles con el modo DirectQuery. Si necesita una determinada función para un cálculo, considere las posibles formas de proporcionar un equivalente usando Transact-SQL.  
  
-   Agregue datos según sea necesario.  Si el modelo utilizaba anteriormente datos de copiar y pegar o datos de proveedores distintos de SQL Server, puede crear nuevas vistas y columnas derivadas dentro de la conexión existente, o utilizar consultas distribuidas.  Todos los datos utilizados en un modelo de DirectQuery deben ser accesibles a través de un único origen de datos de SQL Server.  
  
 **Paso 4. Establecer el método preferido para responder a las consultas en el modelo**  
  
|||  
|-|-|  
|**Solo DirectQuery**|Establezca la propiedad en **DirectQuery**.|  
|**Modo híbrido**|Establezca la propiedad en **In-Memory con DirectQuery** o en **DirectQuery con In-Memory**.<br /><br /> Este valor se puede modificar posteriormente para utilizar otra preferencia.<br /><br /> Observe que los clientes pueden invalidar el método preferido en la cadena de conexión.|  
  
 **Paso 5. Especificar la partición DirectQuery**  
  
|||  
|-|-|  
|**Solo DirectQuery**|Opcional. Un modelo de solo DirectQuery no necesita ninguna partición.<br /><br /> Sin embargo, si ha creado particiones en el modelo durante la fase de diseño, recuerde que solo se puede utilizar una partición como origen de datos. De forma predeterminada, la primera partición que creó se utilizará como la partición de DirectQuery.<br /><br /> Para asegurarse de que todos los datos que necesita el modelo están disponibles en la partición de DirectQuery, elija una partición de DirectQuery y modifique la instrucción SQL para obtener el conjunto de datos completo.|  
|**Modo híbrido**|Si alguna tabla del modelo tiene varias particiones, debe elegir una sola partición como *partición de DirectQuery*. Si no asigna una partición, la primera partición creada se utilizará, de forma predeterminada, como la partición de DirectQuery.<br /><br /> Establezca opciones de procesamiento en todas las particiones salvo en la de DirectQuery. Normalmente, la partición de DirectQuery nunca se procesa, porque los datos se pasan a través del origen relacional.<br /><br /> Para obtener más información, consulte [particiones y el modo DirectQuery &#40;Tabular de SSAS&#41;](tabular-models/define-partitions-in-directquery-models-ssas-tabular.md).|  
  
 **Paso 6. Configurar la suplantación**  
  
 La suplantación solo se admite en los modelos DirectQuery. La opción de suplantación **Configuración de suplantación**define las credenciales que se utilizan al ver los datos del origen de datos de SQL Server especificado.  
  
|||  
|-|-|  
|**Solo DirectQuery**|En la propiedad  **Configuración de suplantación** , especifique la cuenta que se utilizará para conectar con el origen de datos de SQL Server.<br /><br /> Si usa el valor, **ImpersonateCurrentUser**, la instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que hospeda el modelo pasará las credenciales del usuario actual del modelo de la base de datos de SQL Server.|  
|**Modo híbrido**|En la propiedad **Configuración de suplantación** , especifique la cuenta que se utilizará para acceder a los datos del origen de datos de SQL Server.<br /><br /> Esta configuración no afecta a las credenciales utilizadas para procesar la memoria caché usada por el modelo.|  
  
 **Paso 7. Implementar el modelo**  
  
 Cuando esté listo para implementar el modelo, abra el **proyecto** menú de Visual Studio y seleccione **propiedades**. Establezca la propiedad de **QueryMode** en uno de los valores descritos en la siguiente tabla:  
  
 Para obtener más información, consulte [implementar desde SQL Server Data Tools &#40;Tabular de SSAS&#41;](tabular-models/deploy-from-sql-server-data-tools-ssas-tabular.md).  
  
|||  
|-|-|  
|**Solo DirectQuery**|**DirectQueryOnly**<br /><br /> Dado que ha especificado solo Direct Query, los metadatos del modelo se implementarán en el servidor, pero no se procesará el modelo.<br /><br /> Tenga en cuenta que la memoria caché utilizada por la base de datos del área de trabajo no se eliminará automáticamente. Si desea asegurarse de que los usuarios no puedan ver los datos de la memoria caché, borre la caché de tiempo de diseño. Para obtener más información, consulte [borrar las cachés de Analysis Services](instances/clear-the-analysis-services-caches.md).|  
|**Modo híbrido**|**DirectQuery con In-Memory**<br /><br /> **In-Memory con DirectQuery**<br /><br /> Ambos valores le permiten utilizar la memoria caché o el origen de datos relacional según sea necesario. El orden define el origen de datos que se utiliza de forma predeterminada al responder a las consultas realizadas en el modelo.<br /><br /> En un modo híbrido, la memoria caché se debe procesar al mismo tiempo que los metadatos del modelo se implementan en el servidor.<br /><br /> Puede cambiar este valor una vez realizada la implementación.|  
  
 **Paso 8. Comprobar el modelo implementado**  
  
 En [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], abra la instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] en la que implementó el modelo. Haga clic con el botón secundario en el nombre de la base de datos y seleccione **Propiedades**.  
  
-   La propiedad **DirectQueryMode**se estableció al definir las propiedades de implementación.  
  
-   La propiedad **Información de suplantación de origen de datos**se estableció al definir las opciones de suplantación de usuarios. Para más información, vea [Establezca las opciones de suplantación &#40;SSAS - multidimensional&#41;](multidimensional-models/set-impersonation-options-ssas-multidimensional.md).  
  
-   Una vez implementado el modelo, puede cambiar estas propiedades en cualquier momento.  
  
##  <a name="bkmk_Configurations"></a> Comparar las opciones de DirectQuery  
 **Solo DirectQuery**  
 Es preferible utilizar esta opción si se desea garantizar un único origen de datos, o si los datos no caben en la memoria. Si trabaja con un origen de datos relacional muy grande, durante el tiempo de diseño puede crear el modelo utilizando un subconjunto de los datos. Al implementar el modelo en el modo Solo DirectQuery, puede modificar la definición del origen de datos para incluir todos los datos necesarios.  
  
 También es preferible utilizar esta opción si se desea utilizar la seguridad proporcionada por el origen de datos relacional para controlar el acceso de los usuarios a los datos. Con los modelos tabulares almacenados en caché, también puede usar [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] roles para controlar el acceso de datos, pero los datos almacenados en la memoria caché también deben protegerse. Debe utilizar siempre esta opción si el contexto de seguridad requiere que los datos no se almacenen nunca en la memoria caché.  
  
 En la tabla siguiente se describen los posibles resultados de implementación para el modo Solo DirectQuery:  
  
|||  
|-|-|  
|**DirectQuery sin caché**|No se carga ningún dato en la memoria caché. El modelo no se podrá procesar nunca.<br /><br /> Solo se podrán realizar consultas en el modelo utilizando clientes compatibles con las consultas DAX. Los resultados de la consulta siempre se devolverán desde el origen de datos original.<br /><br /> **DirectQueryMode** = `On`<br /><br /> **QueryMode** = **DirectQuery**|  
|**DirectQuery con consultas en caché solo**|Se produce un error en la implementación. No se admite esta configuración.<br /><br /> **DirectQueryMode** = `On`<br /><br /> **QueryMode** = **In-Memory**|  
  
 **Modo híbrido**  
 La implementación del modelo en un modo híbrido tiene muchas ventajas: permite conseguir datos actualizados del origen de datos de SQL Server si es necesario, pero la conservación de la memoria caché le ofrece la posibilidad de trabajar con datos en memoria mientras diseña informes o prueba el modelo, obteniendo un mejor rendimiento.  
  
 Un modo híbrido de DirectQuery también es útil si el modelo es muy grande. Para evitar que los usuarios obtengan datos obsoletos o que no se pueda utilizar el modelo mientras se procesa la memoria caché, puede cambiar el modelo al modo DirectQuery mientras se realiza el procesamiento. Es posible que los usuarios experimenten un rendimiento ligeramente inferior, pero podrán conseguir los datos directamente del almacén relacional, evitando así resultados obsoletos.  
  
 La tabla siguiente compara el resultado de la implementación en cada una de las combinaciones de opciones de DirectQuery.  
  
|||  
|-|-|  
|**Modo híbrido con caché preferida**|El modelo se puede procesar y los datos se pueden cargar en la memoria caché. Las consultas utilizan la memoria caché de forma predeterminada.  Si un cliente desea utilizar el origen de datos DirectQuery, se debe insertar un parámetro en la cadena de conexión.<br /><br /> **DirectQueryMode** = `On`<br /><br /> **QueryMode** = **In-Memory with DirectQuery**|  
|**Modo híbrido con DirectQuery preferido**|El modelo se procesa y los datos se pueden cargar en la memoria caché. Sin embargo, las consultas utilizan DirectQuery de forma predeterminada. Si un cliente desea utilizar los datos en caché, se debe insertar un parámetro en la cadena de conexión. Si las tablas del modelo se dividen en particiones, la partición principal de la memoria caché también se establece en **In-Memory con DirectQuery**.<br /><br /> **DirectQueryMode** = `On`<br /><br /> **QueryMode** = **DirectQuery con In-Memory**|  
  
## <a name="see-also"></a>Vea también  
 [Modo DirectQuery &#40;SSAS tabular&#41;](tabular-models/directquery-mode-ssas-tabular.md)   
 [Acceso a datos de modelos tabulares](tabular-models/tabular-model-data-access.md)  
  
  
