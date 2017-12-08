---
title: Conceder permisos de procesamiento (Analysis Services) | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- permissions [Analysis Services], process
- process permissions [Analysis Services]
ms.assetid: c1531c23-6b46-46a8-9ba3-b6d3f2016443
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 33582b08bd8579d7c2c3318594dcbf877c186757
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="grant-process-permissions-analysis-services"></a>Otorgar permisos de procesamiento (Analysis Services)
  Como administrador, puede crear un rol dedicado para las operaciones de procesamiento de Analysis Services, lo cual le permitirá delegar esa tarea en particular a otros usuarios o a aplicaciones destinadas al procesamiento programado desatendido. Los permisos de procesamiento pueden concederse en los niveles de base de datos, cubo, dimensión y estructura de minería de datos. Salvo que esté trabajando en una base de datos tabular o un cubo muy extenso, le recomendamos que otorgue derechos de procesamiento en el nivel de la base de datos, donde se engloben todos los objetos, incluso aquellos que tengan dependencias entre sí.  
  
 Los permisos se otorgan mediante roles que asocian objetos con permisos y cuentas de usuario o grupo de Windows. Recuerde que los permisos son acumulativos. Si un rol otorga permisos para procesar un cubo, y un segundo rol otorga al mismo usuario permiso para procesar una dimensión, los permisos de los dos roles diferentes se combinan para proporcionar al usuario permiso para procesar el cubo y para procesar la dimensión específica en la base de datos.  
  
> [!IMPORTANT]  
>  Los usuarios cuyo rol solamente disponga de permisos Procesar podrán usar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] para conectarse a [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y procesar objetos. Estas herramientas necesitan el permiso **Read Definition** para tener acceso a los metadatos del objeto. Si no se pueden usar estas herramientas, será preciso usar un script XMLA para ejecutar las operaciones de procesamiento.  
>   
>  También le recomendamos que otorgue permisos de **Read Definition** con fines de prueba. Los usuarios que dispongan de permisos de **Leer definición** y de **Procesar base de datos** podrán procesar objetos en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]de forma interactiva. Para obtener más información, vea [Otorgar permisos Leer definición en metadatos de objetos &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-read-definition-permissions-on-object-metadata-analysis-services.md) .  
  
## <a name="set-processing-permissions-at-the-database-level"></a>Establecer permisos de procesamiento al nivel de la base de datos  
 En esta sección, se describe cómo habilitar el procesamiento por parte de usuarios que no sean administradores para todos los cubos, las dimensiones, las estructuras de minería de datos y los modelos de minería de datos en la base de datos.  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conéctese a la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], abra la carpeta Base de datos y seleccione una base de datos.  
  
2.  Haga clic con el botón derecho en **Roles** | **Nuevo rol**. Escriba un nombre y una descripción.  
  
3.  En el panel **General** , active la casilla **Procesar base de datos** . También puede seleccionar **Leer definición** para habilitar asimismo el procesamiento interactivo mediante una de las herramientas de SQL Server, como [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
4.  En el panel **Pertenencia** , agregue las cuentas de usuario y grupo de Windows que tengan permiso para procesar cualquier objeto en esta base de datos.  
  
5.  Haga clic en **Aceptar** para completar la definición del rol.  
  
## <a name="set-processing-permissions-on-individual-objects"></a>Establecer permisos de procesamiento en objetos individuales  
 Puede establecer permisos de procesamiento en cubos, dimensiones, estructuras o modelos de minería de datos individuales.  
  
 Es posible que el procesamiento no se realice correctamente si excluye objetos que deben procesarse juntos (por ejemplo, si habilita el procesamiento en un cubo, pero no lo hace en sus dimensiones relacionadas). Dado que puede resultar sencillo pasar por alto algunas dependencias de objetos, es esencial que se realicen pruebas meticulosas cuando se establecen permisos de procesamiento en objetos individuales.  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conéctese a la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], abra la carpeta Base de datos y seleccione una base de datos.  
  
2.  Haga clic con el botón derecho en **Roles** | **Nuevo rol**. Escriba un nombre y una descripción.  
  
3.  En el panel **General** , desactive la casilla **Procesar base de datos** . Los permisos de base de datos invalidan la capacidad de establecer permisos en objetos de niveles más bajos, de forma que aparecen las opciones de rol sombreadas en gris o sin posibilidad de seleccionarse.  
  
     Técnicamente, no se necesitan permisos de base de datos para los roles de procesamiento dedicados. Pero sin el permiso **Leer definición** en el nivel de la base de datos, no podrá ver la base de datos en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], de forma que la realización de pruebas se hará más difícil.  
  
4.  Seleccione objetos individuales para su procesamiento:  
  
    -   En el panel **Cubos** , active la casilla **Procesar** para cada uno de los cubos.  
  
    -   En el panel **Dimensiones** , active **Todas las dimensiones de la base de datos**y, después, la casilla **Procesar** para cada una de las dimensiones. O bien, seleccione todas las filas, y luego use MAYÚS y clic para alternar entre las selecciones de las casillas.  
  
5.  En el panel **Pertenencia** , agregue las cuentas de usuario y grupo de Windows que tengan permiso para procesar estos objetos.  
  
6.  Haga clic en **Aceptar** para completar la definición del rol.  
  
## <a name="test-processing"></a>Probar el procesamiento  
  
1.  Mantenga pulsada la tecla MAYÚS y haga clic con el botón derecho en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], seleccione **Ejecutar como otro usuario** y conéctese a la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] con una cuenta de Windows que esté asignada al rol que va a probar.  
  
2.  Abra la carpeta Bases de datos y seleccione una base de datos. Solamente podrá ver las bases de datos visibles para los roles para los que la cuenta tiene pertenencia.  
  
3.  Haga clic con el botón derecho en un cubo o una dimensión y seleccione **Procesar**. Elija una opción de procesamiento. Pruebe todas las opciones para todas las combinaciones de objetos. Si se producen errores porque faltan objetos, agregue los objetos al rol.  
  
## <a name="set-processing-permissions-on-a-data-mining-structure"></a>Establecer permisos de procesamiento en una estructura de minería de datos  
 Puede crear un rol que otorgue permisos para procesar estructuras de minería de datos. Esto incluye el procesamiento de todos los modelos de minería.  
  
 Los permisos **Obtener detalles** y **Leer definición** que se usan para examinar modelos y estructuras de minería de datos son atómicos y se pueden agregar al mismo rol o separarse en un rol diferente.  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conéctese a la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], abra la carpeta Base de datos y seleccione una base de datos.  
  
2.  Haga clic con el botón derecho en **Roles** | **Nuevo rol**. Escriba un nombre y una descripción. En el panel **General** , asegúrese de que las casillas de los permisos para la base de datos no están activadas. Los permisos de base de datos invalidarán la capacidad de establecer permisos en objetos de niveles más bajos, de forma que aparecen las opciones de rol sombreadas en gris o sin posibilidad de seleccionarse.  
  
3.  En el panel **Estructuras de minería de datos** , active la casilla **Procesar** para cada una de las estructuras de minería de datos.  
  
4.  En el panel **Pertenencia** , agregue las cuentas de usuario y grupo de Windows que tengan permiso para procesar cualquier objeto en esta base de datos.  
  
5.  Haga clic en **Aceptar** para completar la definición del rol.  
  
## <a name="see-also"></a>Vea también  
 [Procesar base de datos, tabla o partición &#40;Analysis Services&#41;](../../analysis-services/tabular-models/process-database-table-or-partition-analysis-services.md)   
 [Procesar un modelo multidimensional &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)   
 [Otorgar permisos de base de datos &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-database-permissions-analysis-services.md)   
 [Otorgar permisos Leer definición en metadatos de objetos &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-read-definition-permissions-on-object-metadata-analysis-services.md)  
  
  
