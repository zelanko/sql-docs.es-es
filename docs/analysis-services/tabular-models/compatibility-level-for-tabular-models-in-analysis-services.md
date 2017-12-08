---
title: Nivel de compatibilidad para los modelos tabulares en Analysis Services | Documentos de Microsoft
ms.custom: 
ms.date: 10/16/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.asvs.bidtoolset.versioncompat.f1
ms.assetid: 8943d78d-4a73-4be8-ad14-3d428f5abd06
caps.latest.revision: "27"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 385d9a062dfa723e4e73317ffca6984b18f22c47
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="compatibility-level-for-analysis-services-tabular-models"></a>Nivel de compatibilidad para los modelos tabulares de Analysis Services
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  El *nivel de compatibilidad* hace referencia a comportamientos específicos de la versión en el motor de Analysis Services. Por ejemplo, los metadatos de objetos tabulares y de DirectQuery tienen implementaciones diferentes según el nivel de compatibilidad. En general, debe elegir el nivel de compatibilidad más reciente compatible con los servidores.

  **El nivel de compatibilidad más reciente es 1400** 
  
Características principales en el nivel de compatibilidad de 1400 incluyen:

*  Nueva infraestructura para la conectividad de datos e importarlos en los modelos tabulares con compatibilidad para TOM APIs y secuencias de comandos de TMSL. Esto habilita la compatibilidad con orígenes de datos adicionales, como el almacenamiento de blobs de Azure. Los orígenes de datos adicionales incluyen en futuras actualizaciones.
*  Transformación de datos y capacidades de mashup de datos mediante el uso de expresiones de obtención de datos y M.
*  Medidas ahora admiten una propiedad de las filas de detalles con una expresión de DAX, habilitar herramientas de BI como Microsoft Excel exploración en profundidad para datos detallados de un informe de agregado. Por ejemplo, cuando los usuarios finales ver total de ventas de una región y el mes, pueden ver los detalles del pedido asociados. 
*  Seguridad de nivel de objeto para los nombres de tabla y columna, además de los datos dentro de ellos.
*  Compatibilidad mejorada para las jerarquías desiguales.
*  Supervisión del rendimiento y mejoras.

  
## <a name="supported-compatibility-levels-by-version"></a>Niveles de compatibilidad admitidos por versión
  
|||  
|-|-|- 
|**Nivel de compatibilidad**|**Versión del servidor**| 
|1400|Servicios de análisis de Azure, SQL Server de 2017 |  
|1200|Servicios de análisis de Azure, SQL Server de 2017, SQL Server 2016| 
|1103|SQL Server de 2017 *, SQL Server 2016, SQL Server 2014, SQL Server 2012 SP1|  
|1100|SQL Server de 2017 *, SQL Server 2016, SQL Server 2014, SQL Server 2012 SP1, SQL Server 2012| 

\*niveles de compatibilidad 1100 y 1103 están desusados en SQL Server 2017.
  
## <a name="set-compatibility-level"></a>Definir el nivel de compatibilidad 
 Al crear un nuevo proyecto de modelo tabular en SQL Server Data Tools (SSDT), puede especificar el nivel de compatibilidad en el **Diseñador de modelos tabulares** cuadro de diálogo. 
  
 ![ssas_tabularproject_compat1200](../../analysis-services/tabular-models/media/ssas-tabularproject-compat1200.png)  
  
 Si selecciona el **no volver a mostrar este mensaje** opción, todos los proyectos posteriores usarán el nivel de compatibilidad que especificó como el valor predeterminado. Puede cambiar el nivel de compatibilidad predeterminado en SSDT en **Herramientas** > **Opciones**.  
  
 Para actualizar un proyecto de modelo tabular en SSDT, establezca el **nivel de compatibilidad** propiedad en el modelo **propiedades** ventana. Tenga en cuenta que, el nivel de compatibilidad de la actualización es irreversible.
  
## <a name="check-compatibility-level-for-a-database-in-ssms"></a>Comprobar el nivel de compatibilidad para una base de datos en SSMS  
 En SSMS, haga clic en el nombre de la base de datos > **propiedades** > **nivel de compatibilidad**.  
  
## <a name="check-supported-compatibility-level-for-a-server-in-ssms"></a>Comprobar el nivel de compatibilidad admitido para un servidor en SSMS  
 En SSMS, haga clic con el botón derecho en el nombre del servidor > **Propiedades** > **Nivel de compatibilidad admitido**.  
  
 Esta propiedad especifica el máximo nivel de compatibilidad de una base de datos que se ejecutará en el servidor. El nivel de compatibilidad admitido es de solo lectura y no se puede cambiar.  
  
## <a name="see-also"></a>Vea también  
 [Nivel de compatibilidad de una base de datos multidimensional](../../analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services.md)   
 [Novedades de Analysis Services](../../analysis-services/what-s-new-in-analysis-services.md)   
 [Cree un nuevo proyecto de modelo tabular](../../analysis-services/tabular-models/create-a-new-tabular-model-project-analysis-services.md)  
  
  
