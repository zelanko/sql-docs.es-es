---
title: Conceder acceso personalizado a los datos de las celdas (Analysis Services) | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 575f2f0e4d0d13a3a27e359125584a185d932122
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="grant-custom-access-to-cell-data-analysis-services"></a>Otorgar acceso personalizado a los datos de las celdas (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  La seguridad de celdas se usa para permitir o denegar el acceso para medir los datos de un cubo. En la siguiente ilustración presentamos una combinación de medidas permitidas y denegadas en una tabla dinámica, cuando se está conectado como usuario con un rol que solamente permite el acceso a ciertas medidas. En este ejemplo, **Importe de venta del distribuidor** y **Coste total del producto del distribuidor** son las únicas medidas disponibles mediante este rol. El resto de medidas se deniegan de forma implícita (los pasos que se siguen para obtener este resultado se describen a continuación, en la sección siguiente: Permitir el acceso a medidas específicas).  
  
 ![Tabla dinámica que muestra celdas permitidas y denegadas](../../analysis-services/multidimensional-models/media/ssas-permscellsallowed.png "tabla dinámica que muestra celdas permitidas y denegadas")  
  
 Los permisos de celda se aplican a los datos en el interior de la celda y no a sus metadatos. Fíjese cómo la celda sigue visible en los resultados de una consulta, con un valor de **#N/A** en lugar del valor real de la celda. El valor **#N/A** aparece en la celda, a no ser que la aplicación cliente convierta el valor o que se especifique otro valor estableciendo la propiedad Secured Cell Value en la cadena de conexión.  
  
 Para ocultar completamente la celda, tiene que limitar los miembros (dimensiones, atributos de dimensión y miembros de atributo de dimensión) que se pueden ver. Para obtener más información, vea [Conceder acceso personalizado a datos de dimensión &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-dimension-data-analysis-services.md).  
  
 Como administrador, puede especificar si los miembros del rol van a tener permisos de Lectura, Contingente de lectura o Lectura y escritura. Conferir permisos a una celda es tan solo el nivel inferior de seguridad permitido, por tanto, antes de comenzar a aplicar permisos en este nivel, es importante que tenga en cuenta diversos aspectos:  
  
-   La seguridad de nivel de celda no puede expandir los derechos que se hayan restringido a un nivel superior. Un jemplo: si un rol deniega el acceso a los datos de dimensiones, la seguridad a nivel de celda no puede invalidar el conjunto que se ha denegado. Otro ejemplo: si se trata de un rol con permiso de **Lectura** en un cubo y permiso de **Lectura y escritura** en una celda, el permiso de datos de la celda no será **Lectura y escritura**, sino que será **Lectura**.  
  
-   Los permisos personalizados, por lo general, se deben coordinar entre miembros de dimensión y celdas en el mismo rol. Por ejemplo, si quiere denegar el acceso a diversas medidas relacionadas con descuentos correspondientes a diferentes combinaciones de distribuidores. Con los **Distribuidores** como datos de dimensión y el **Importe de descuento** como medida, debería combinar, dentro del mismo rol, permisos en la medida (con la ayuda de las instrucciones de este tema) y en los miembros de dimensión. Vea [Conceder acceso personalizado a datos de dimensión &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-dimension-data-analysis-services.md) para obtener más información sobre cómo establecer permisos de dimensión.  
  
 La seguridad a nivel de celda se especifica a través de expresiones MDX. Dado que la celda es una tupla (o sea, un punto de intersección potencialmente en varias dimensiones y medidas), es necesario usar MDX para identificar celdas específicas.  
  
## <a name="allow-access-to-specific-measures"></a>Permitir el acceso a medidas específicas  
 Puede usar la seguridad de celda para elegir explícitamente qué medidas estarán disponibles. Una vez que haya identificado específicamente los miembros que se permiten, el resto de medidas pasa a no estar disponible. Se trata quizás del escenario más sencillo para realizar implementaciones a través de scripts MDX, tal como se describe en los pasos siguientes.  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , conéctese a la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], seleccione una base de datos, abra la carpeta **Roles** y, después, haga clic en un rol de base de datos (o cree un rol de base de datos nuevo). La pertenencia ya debería estar especificada y el rol debería tener acceso de **Read** al cubo. Vea [Otorgar permisos para cubos o modelos &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-cube-or-model-permissions-analysis-services.md) si necesita ayuda con este paso.  
  
2.  En **Datos de celda**, compruebe la selección del cubo para asegurarse de que ha elegido el correcto y, después, seleccione **Habilitar permisos de lectura**.  
  
     Si activa únicamente esta casilla y no proporciona una expresión MDX, el resultado será el mismo que si deniega el acceso a todas las celdas del cubo. Esto se debe a que el conjunto permitido predeterminado es un conjunto vacío siempre que [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de como resultado un subconjunto de celdas de cubo.  
  
3.  Especifique la siguiente expresión MDX.  
  
    ```  
    (Measures.CurrentMember IS [Measures].[Reseller Sales Amount]) OR (Measures.CurrentMember IS [Measures].[Reseller Total Product Cost])  
    ```  
  
     La expresión identifica explícitamente las medidas que verán los usuarios. No estarán disponibles otras medidas para los usuarios que se conecten mediante este rol. Tenga en cuenta que [CurrentMember &#40;MDX&#41;](../../mdx/currentmember-mdx.md) establece el contexto y está seguido de la medida permitida. El efecto de esta expresión es mostrar el valor, en caso de que el miembro actual incluya el **Importe de venta del distribuidor** o el **Coste total del producto del distribuidor**. De lo contrario, denegará el acceso. La expresión consta de varias partes, cada una de ellas entre paréntesis. El operador **OR** se usa para especificar varias medidas.  
  
## <a name="deny-access-to-specific-measures"></a>Denegar el acceso a medidas específicas  
 La siguiente expresión MDX, también especificada en **Crear rol** | **Datos de celda** | **Permitir la lectura del contenido del cubo**, tiene el efecto contrario; hacer que ciertas medidas no estén disponibles. En este ejemplo, **Importe de descuento** y **Porcentaje de descuento** se han inhabilitado mediante los operadores **NOT** y **AND** . El resto de medidas estará visible para los usuarios que se conecten mediante este rol.  
  
```  
(NOT Measures.CurrentMember IS [Measures].[Discount Amount]) AND (NOT Measures.CurrentMember IS [Measures].[Discount Percentage])  
```  
  
 En Excel, la seguridad de celda se hace patente en la ilustración siguiente:  
  
 ![Columnas que muestran celdas como no disponible en Excel](../../analysis-services/multidimensional-models/media/ssas-permscellshidemeasure.png "columnas que muestran celdas como no disponible en Excel")  
  
## <a name="set-read-permissions-on-calculated-measures"></a>Establecer permisos de Lectura en medidas calculadas  
 Los permisos en medidas calculadas se pueden establecer independientemente de sus partes constituyentes. Si quiere coordinar los permisos entre una medida calculada y sus medidas dependientes, pase a la siguiente sección sobre Contingente de lectura.  
  
 Para saber como actúan los permisos de Lectura en una medida calculada, remítase a **Reseller Gross Profit** de AdventureWorks. Se deriva de las medidas **Reseller Sales Amount** y **Reseller Total Product Cost** . Siempre que un rol tenga permiso de Lectura en celdas **Reseller Gross Profit** , se podrá ver esta medida incluso si los permisos se han denegado expresamente en otras medidas. Para ver una demostración, copie la siguiente expresión MDX en **Crear rol** | **Datos de celda** | **Permitir lectura de contenido del cubo**.  
  
```  
(NOT Measures.CurrentMember IS [Measures].[Reseller Sales Amount])  
AND (NOT Measures.CurrentMember IS [Measures].[Reseller Total Product Cost])  
```  
  
 En Excel, conéctese al cubo con el rol actual y elija las tres medidas para ver el resultado de la seguridad de celda. Vea que las medidas en el conjunto que se ha denegado no están disponibles, pero el usuario puede ver la medida calculada.  
  
 ![Tabla de Excel con disponibles y no cellls](../../analysis-services/multidimensional-models/media/ssas-permscalculatedcells.png "tabla de Excel con cellls disponible y no está disponible")  
  
## <a name="set-read-contingent-permissions-on-calculated-measures"></a>Establecer permisos de Contingente de lectura en medidas calculadas  
 La seguridad de celda ofrece una alternativa, Contingente de lectura, para establecer permisos en las celdas asociadas que participan en un cálculo. Remítase de nuevo al ejemplo de **Reseller Gross Profit** . Al especificar la misma expresión MDX que se proporciona en la sección anterior, colóquela esta vez en la segunda área de texto del cuadro de diálogo **Crear rol** | **Datos de celda** (en el área de texto inferior **Permitir la lectura del contenido de la celda supeditado a la seguridad de celda**), el resultado aparece cuando se ve en Excel. Dado que **Reseller Gross Profit** depende de **Reseller Sales Amount** y **Reseller Total Product Cost**, ahora no se puede tener acceso al beneficio bruto porque no se tiene acceso a sus partes constituyentes.  
  
> [!NOTE]  
>  ¿Qué sucede si se establecen los permisos de Lectura y Contingente de lectura en una celda dentro del mismo rol? El rol concederá permisos de Lectura en la celda, pero no de Contingente de lectura.  
  
 En secciones anteriores, se había indicado que cuando se activa solamente la casilla **Habilitar permisos de contingente de lectura** sin especificar una expresión MDX, se denegaba el acceso a todas las celdas del cubo. Esto se debe a que el conjunto permitido predeterminado es un conjunto vacío siempre que [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de como resultado un subconjunto de celdas de cubo.  
  
## <a name="set-readwrite-permissions-on-a-cell"></a>Establecer permisos de Lectura y escritura en una celda  
 Los permisos de Lectura y escritura en una celda se usan para habilitar la reescritura, siempre que los miembros tengan permisos de Lectura y escritura para el propio cubo. Los permisos que se conceden en las celdas no pueden ser superiores a los permisos concedidos en un cubo. Para obtener información detallada, vea [Set Partition Writeback](../../analysis-services/multidimensional-models/set-partition-writeback.md) .  
  
## <a name="see-also"></a>Vea también  
 [Generador MDX &#40;Analysis Services - Datos multidimensionales&#41;](http://msdn.microsoft.com/library/fecbf093-65ea-4e1b-b637-f04876f1cb0f)   
 [El Script MDX básico & #40; MDX & #41;](../../analysis-services/multidimensional-models/mdx/the-basic-mdx-script-mdx.md)   
 [Conceder permisos de procesamiento &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-process-permissions-analysis-services.md)   
 [Conceder permisos para una dimensión &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-permissions-on-a-dimension-analysis-services.md)   
 [Conceder acceso personalizado a la dimensión de datos & #40; Analysis Services & #41;](../../analysis-services/multidimensional-models/grant-custom-access-to-dimension-data-analysis-services.md)   
 [Conceder el cubo o modelo permisos & #40; Analysis Services & #41;](../../analysis-services/multidimensional-models/grant-cube-or-model-permissions-analysis-services.md)  
  
  
