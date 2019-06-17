---
title: Nivel de compatibilidad para modelos tabulares de Analysis Services | Microsoft Docs
ms.date: 06/10/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 19c69aa1a1ab27e7498d3c9d6a0d52c25b9f0020
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66826833"
---
# <a name="compatibility-level-for-analysis-services-tabular-models"></a>Nivel de compatibilidad para modelos tabulares de Analysis Services
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]

  El *ivel* hace referencia a las mejoras de funcionalidad y características en el motor de Analysis Services y en los metadatos del modelo tabular. En general, debe elegir el nivel de compatibilidad más reciente compatible con los servidores. 

  **El nivel de compatibilidad admitido más reciente es el 1400** 
  
Las características principales en el nivel de compatibilidad 1400 incluyen:

*  Nueva infraestructura para la conectividad de datos e importarlos en modelos tabulares con compatibilidad con TOM APIs y scripting de TMSL. Esto habilita la compatibilidad con orígenes de datos adicionales, como Azure Blob storage. Los orígenes de datos adicionales incluyen en futuras actualizaciones.
*  Transformación de datos y capacidades de mashup de datos mediante el uso de expresiones Get Data y m. en SQL Server Data Tools (SSDT).
*  Mide ahora compatibilidad con una propiedad de filas de detalles con una expresión de DAX, habilitar a BI de las herramientas como Microsoft Excel análisis detallado de datos de un informe agregado detallados. Por ejemplo, cuando los usuarios ven las ventas totales de una región y mes, pueden ver los detalles del pedido asociados. 
*  Seguridad de nivel de objeto para los nombres de tabla y columna, además de los datos dentro de ellos.
*  Compatibilidad mejorada para las jerarquías desiguales.
*  Supervisión del rendimiento y mejoras.

  
## <a name="supported-compatibility-levels-by-version"></a>Niveles de compatibilidad admitidos por versión
  
Niveles de compatibilidad inferiores son compatibles con versiones anteriores de compatibilidad. 

|||  
|-|-|- 
|**Nivel de compatibilidad**|**Versión del servidor**| 
|1470|SQL Server 2019 (CTP 2.3 y versiones posterior) | 
|1400|Azure Analysis Services, SQL Server 2019, SQL Server 2017 |  
|1200|Azure Analysis Services, SQL Server 2019, SQL Server 2017, SQL Server 2016| 
|1103|SQL Server 2017*, SQL Server 2016, SQL Server 2014, SQL Server 2012 SP1|  
|1100|SQL Server 2017*, SQL Server 2016, SQL Server 2014, SQL Server 2012 SP1, SQL Server 2012| 

\* niveles de compatibilidad 1100 y 1103 están en desuso en SQL Server 2017 y versiones posteriores.
  
## <a name="set-compatibility-level"></a>Establecimiento del nivel de compatibilidad 
 Al crear un nuevo proyecto de modelo tabular en SQL Server Data Tools (SSDT), puede especificar el nivel de compatibilidad en el **Diseñador de modelos tabulares** cuadro de diálogo. 
  
 ![ssas_tabularproject_compat1200](../../analysis-services/tabular-models/media/ssas-tabularproject-compat1200.png)  
  
 Si selecciona el **no volver a mostrar este mensaje** opción, todos los proyectos posteriores usarán el nivel de compatibilidad que especificó como el valor predeterminado. Puede cambiar el nivel de compatibilidad predeterminado en SSDT en **Herramientas** > **Opciones**.  
  
 Para actualizar un proyecto de modelo tabular en SSDT, establezca el **ivel** propiedad en el modelo **propiedades** ventana. Tenga en cuenta que, actualizar el nivel de compatibilidad es irreversible.
  
## <a name="check-compatibility-level-for-a-database-in-ssms"></a>Comprobar el nivel de compatibilidad para una base de datos en SSMS  
 En SSMS, haga clic en el nombre de la base de datos > **propiedades** > **ivel**.  
  
## <a name="check-supported-compatibility-level-for-a-server-in-ssms"></a>Comprobar el nivel de compatibilidad admitido para un servidor en SSMS  
 En SSMS, haga clic con el botón derecho en el nombre del servidor > **Propiedades** > **Nivel de compatibilidad admitido**.  

 Esta propiedad especifica el máximo nivel de compatibilidad de una base de datos que se ejecutará en el servidor. El nivel de compatibilidad admitido es de solo lectura y no se puede cambiar.
 
> [!NOTE]  
>  En SSMS, cuando se conecta a un servidor SQL Server Analysis Services, el servidor de Azure Analysis Services o el área de trabajo de Power BI Premium, la propiedad de nivel de compatibilidad admitido mostrará 1200. Esto es un problema conocido y se resolverá en una próxima SSMS update. Cuando se resuelva, esta propiedad mostrará el máximo nivel de compatibilidad admitido. 
  
## <a name="see-also"></a>Vea también  
 [Nivel de compatibilidad de una base de datos multidimensional](../../analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services.md)   
 [What's new in Analysis Services](../../analysis-services/what-s-new-in-analysis-services.md)   
 [Cree un nuevo proyecto de modelo tabular](../../analysis-services/tabular-models/create-a-new-tabular-model-project-analysis-services.md)  
  
  
