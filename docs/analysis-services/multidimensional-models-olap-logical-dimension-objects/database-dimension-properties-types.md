---
title: Tipos de dimensiones | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 663c26ac169c11e5ab2d9b90285419cf4145368c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63025770"
---
# <a name="database-dimension-properties---types"></a>Propiedades de la dimensión de base de datos: tipos
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  El **tipo** configuración de la propiedad proporciona información sobre el contenido de una dimensión en aplicaciones cliente y servidor. En algunos casos, el **tipo** configuración solo se proporcionan instrucciones para las aplicaciones cliente y es opcional. En otros casos, como **cuentas** o **tiempo** dimensiones, el **tipo** valores de propiedad de la dimensión y sus atributos determinan comportamientos específicos basados en servidor y puede ser necesario implementar ciertos comportamientos del cubo. Por ejemplo, el **tipo** se puede establecer la propiedad de una dimensión **cuentas** para indicar a las aplicaciones cliente que la dimensión estándar contiene atributos de cuenta. Para obtener más información sobre el tiempo, la cuenta y las dimensiones de moneda, vea [crear una dimensión de tipo Date](../../analysis-services/multidimensional-models/database-dimensions-create-a-date-type-dimension.md), [crear una cuenta financiera de dimensión de tipo de elementos primarios y secundarios](../../analysis-services/multidimensional-models/database-dimensions-finance-account-of-parent-child-type.md), y [crear una moneda tipo de dimensión](../../analysis-services/multidimensional-models/database-dimensions-create-a-currency-type-dimension.md).  
  
 El valor predeterminado para el tipo de dimensión es **Regular**, que no hace suposiciones sobre el contenido de la dimensión. Esta es la configuración predeterminada para todas las dimensiones al definir inicialmente una dimensión a menos que especifique **tiempo** al definir la dimensión mediante el Asistente para dimensiones. También se debe dejar **Regular** como el tipo de dimensión si el Asistente para dimensiones no muestra un tipo adecuado para el tipo de dimensión.  
  
## <a name="available-dimension-types"></a>Tipos de dimensiones disponibles  
 La tabla siguiente describen los tipos de dimensiones disponibles en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
|Tipo de dimensión|Descripción|  
|--------------------|-----------------|  
|Regular|Dimensión cuyo tipo no se ha establecido en un tipo de dimensión especial.|  
|Time|Dimensión cuyos atributos representan periodos de tiempo, como años, semestres, trimestres, meses y días.|  
|Organización|Dimensión cuyos atributos representan información organizativa, como empleados o subsidiarias.|  
|Geografía|Dimensión cuyos atributos representan información geográfica, como ciudades o códigos postales.|  
|Lista de materiales|Dimensión cuyos atributos representan información de inventario o de fabricación, como listas de piezas para productos.|  
|Cuentas|Dimensión cuyos atributos representan un gráfico de cuentas para la elaboración de informes financieros.|  
|Clientes|Dimensión cuyos atributos representan información de clientes o de contacto.|  
|Productos|Dimensión cuyos atributos representan información de productos.|  
|Escenario|Dimensión cuyos atributos representan información de planeación o análisis estratégico.|  
|Cuantitativo|Dimensión cuyos atributos representan información cuantitativa.|  
|Utilidad|Dimensión cuyos atributos representan información diversa.|  
|Currency|Este tipo de dimensión contiene datos de moneda y metadatos.|  
|Tarifas|Dimensión cuyos atributos representan información de tasa de cambio.|  
|Canal|Dimensión cuyos atributos representan información de canal.|  
|Promoción|Dimensión cuyos atributos representan información de promociones de marketing.|  
  
## <a name="see-also"></a>Vea también  
 [Crear una dimensión mediante el uso de una tabla existente](../../analysis-services/multidimensional-models/create-a-dimension-by-using-an-existing-table.md)   
 [Dimensiones &#40;Analysis Services - Datos multidimensionales&#41;](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)  
  
  
