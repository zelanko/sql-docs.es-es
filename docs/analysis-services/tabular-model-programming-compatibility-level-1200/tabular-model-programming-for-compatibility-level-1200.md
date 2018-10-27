---
title: Programación de modelos tabulares de nivel de compatibilidad 1200 | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4f1ab3b825ad85d490493c1ffa05d7e066ec0cce
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/26/2018
ms.locfileid: "50144764"
---
# <a name="tabular-model-programming-for-compatibility-level-1200-and-higher"></a>Programación de modelos tabulares para el nivel de compatibilidad 1200 y posteriores
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
A partir de nivel de compatibilidad 1200, los metadatos tabulares se usan para describir construcciones de modelo, reemplazando históricos metadatos multidimensionales como descriptores de objetos de modelo Tabular. Los metadatos de tablas, columnas y relaciones son de tabla, columna y relación, en lugar de los equivalentes de Multidimensional (dimensión y atributo).  
  
Puede crear nuevos modelos de nivel de compatibilidad 1200 o superior con las APIs Microsoft.AnalysisServices.Tabular, la versión más reciente de SQL Server Data Tools (SSDT), o cambiando el **CompatibilityLevel** de un Tabular existente modelo para actualizarlo (que también se hace en SSDT). Si lo hace, enlaza el modelo a las versiones más recientes del servidor, herramientas y las interfaces de programación.   
  
Actualizar una solución Tabular existente se recomienda, aunque no es necesario. Script existente y soluciones personalizadas que acceder o administran los modelos tabulares o las bases de datos pueden usarse como-es. Niveles de compatibilidad menores son totalmente compatibles en SQL Server 2016 mediante las características disponibles en ese nivel. Azure Analysis Services solo admite el nivel de compatibilidad 1200 y superior.
  
 Nuevos modelos tabulares requieren código diferente y script, se resumen a continuación.  
  
## <a name="object-model-definitions-as-tabular-metadata-constructs"></a>Definiciones de modelo de objetos como construcciones de metadatos tabulares  
 El modelo de objetos tabulares para los modelos 1200 o superiores se expone en JSON por medio del [Tabular Model Scripting Language](https://docs.microsoft.com/bi-reference/tmsl/tabular-model-scripting-language-tmsl-reference) y mediante el lenguaje de definición de datos AMO a través de un nuevo espacio de nombres, [ Microsoft.AnalysisServices.Tabular](http://msdn.microsoft.com/library/microsoft.analysisservices.tabular.aspx)

## <a name="script-for-tabular-models-and-databases"></a>Secuencia de comandos para los modelos tabulares y bases de datos  
 TMSL es un lenguaje de scripting JSON para los modelos tabulares, con compatibilidad para la creación, lectura, actualización y las operaciones de una eliminación. Puede actualizar los datos a través de TMSL e invocar operaciones de base de datos para adjuntar, separar, copia de seguridad, restauración y sincronizar.  
  
 AMO PowerShell acepta script TMSL como entrada.  
  
 Consulte [Tabular Model Scripting Language &#40;TMSL&#41; referencia](https://docs.microsoft.com/bi-reference/tmsl/tabular-model-scripting-language-tmsl-reference) y [Analysis Services PowerShell Reference](../../analysis-services/powershell/analysis-services-powershell-reference.md) para obtener más información.  
  
## <a name="query-languages"></a>Lenguajes de consulta  
 DAX y MDX se admiten para todos los modelos tabulares.  
  
## <a name="expression-language"></a>Lenguaje de expresiones  
 Los filtros y las expresiones usadas para crear los objetos calculados, incluidas las medidas y KPI, se formulan en DAX. Consulte [descripción de DAX en modelos tabulares](../../analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular.md) y [expresiones de análisis de datos &#40;DAX&#41; en Analysis Services](http://msdn.microsoft.com/library/abb336c9-3346-4cab-b91b-90f93f4575e5).  
  
## <a name="managed-code-for-tabular-models-and-databases"></a>Código administrado para los modelos tabulares y bases de datos  
 AMO incluye un nuevo espacio de nombres, Microsoft.AnalysisServices.Tabular, para trabajar con modelos mediante programación. Consulte [Microsoft.AnalysisServices Namespace](https://msdn.microsoft.com/library/ms146720\(SQL.130\).aspx) para obtener más información.  
  
> [!NOTE]  
>  El tiempo de ejecución de .NET 4.0 ahora apuntan a las bibliotecas de cliente de Analysis Services Management Objects (AMO), ADOMD.NET y el modelo de objetos tabulares (TOM).   
  
## <a name="see-also"></a>Vea también  
 [Guía del desarrollador (Analysis Services)](../../analysis-services/analysis-services-developer-documentation.md)   
 [Programación de modelos tabulares para la compatibilidad de los niveles de 1050 a 1103](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/tabular-model-programming-for-compatibility-levels-1050-through-1103.md)   
 [Referencia técnica ](../../analysis-services/powershell/technical-reference-ssas.md) [actualizar Analysis Services](../../database-engine/install-windows/upgrade-analysis-services.md)  
 [Niveles de compatibilidad de los modelos tabulares y bases de datos](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/tabular-model-programming-for-compatibility-levels-1050-through-1103.md)  
  
  
