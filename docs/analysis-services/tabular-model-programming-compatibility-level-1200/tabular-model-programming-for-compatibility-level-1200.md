---
title: Programación de modelo tabular de nivel de compatibilidad 1200 | Documentos de Microsoft
ms.custom: ''
ms.date: 05/30/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: d343f693-c800-42fe-bb4f-2c38a10919f1
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 171106f6b1cb34631c3a785c1967844574c7fc4a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="tabular-model-programming-for-compatibility-level-1200-and-higher"></a>Programación de modelo tabulares de 1200 de nivel de compatibilidad y versiones posteriores
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
A partir de nivel de compatibilidad 1200, metadatos tabulares se utilizan para describir las construcciones del modelo, reemplazando históricos metadatos multidimensionales como descriptores de objetos de modelo Tabular. Metadatos de tablas, columnas y relaciones son tabla, columna y relación, en lugar de los equivalentes multidimensionales (dimensión y atributo).  
  
Puede crear nuevos modelos de nivel de compatibilidad 1200 o superior mediante las APIs Microsoft.AnalysisServices.Tabular, la versión más reciente de SQL Server Data Tools (SSDT), o cambiando la **CompatibilityLevel** de un Tabular existente modelo para actualizarlo (que también se hace en SSDT). Si lo hace, enlaza el modelo a las versiones más recientes de servidor, herramientas y las interfaces de programación.   
  
Actualizar una solución Tabular existente se recomienda, aunque no es necesario. Secuencia de comandos existente y las soluciones personalizadas que tener acceso o administran los modelos tabulares o las bases de datos pueden utilizarse como-es. Niveles de compatibilidad inferiores son totalmente compatibles con SQL Server 2016 mediante las características disponibles en ese nivel. Azure Analysis Services solo admite el nivel de compatibilidad 1200 y versiones posterior.
  
 Nuevos modelos tabulares requerirá código diferente y los scripts, a continuación.  
  
## <a name="object-model-definitions-as-tabular-metadata-constructs"></a>Definiciones de modelo de objetos como construcciones de metadatos tabulares  
 El modelo de objetos Tabular para los modelos 1200 o superiores se expone en JSON a través de la [Tabular Model Scripting Language](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md) y con el lenguaje de definición de datos AMO a través de un nuevo espacio de nombres, [ Microsoft.AnalysisServices.Tabular](http://msdn.microsoft.com/library/microsoft.analysisservices.tabular.aspx)

## <a name="script-for-tabular-models-and-databases"></a>Secuencia de comandos para los modelos tabulares y las bases de datos  
 TMSL es un lenguaje de scripting de JSON para los modelos tabulares, con compatibilidad para crear, leer, actualizar, un operaciones de eliminación. Puede actualizar los datos a través de TMSL e invoque las operaciones de base de datos para adjuntar, separar, copia de seguridad, restauración y sincronizar.  
  
 AMO PowerShell acepta un script de TMSL como entrada.  
  
 Vea [Tabular Model Scripting Language &#40;TMSL&#41; referencia](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md) y [Analysis Services PowerShell Reference](../../analysis-services/powershell/analysis-services-powershell-reference.md) para obtener más información.  
  
## <a name="query-languages"></a>Lenguajes de consulta  
 DAX y MDX se admiten para todos los modelos tabulares.  
  
## <a name="expression-language"></a>Lenguaje de expresiones  
 Los filtros y las expresiones utilizadas para crear objetos calculados, incluidas las medidas y KPI, se formulan en DAX. Vea [descripción de DAX en modelos tabulares](../../analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular.md) y [expresiones de análisis de datos &#40;DAX&#41; en Analysis Services](http://msdn.microsoft.com/library/abb336c9-3346-4cab-b91b-90f93f4575e5).  
  
## <a name="managed-code-for-tabular-models-and-databases"></a>Código administrado para los modelos tabulares y las bases de datos  
 AMO incluye un nuevo espacio de nombres, Microsoft.AnalysisServices.Tabular, para trabajar con modelos mediante programación. Vea [Microsoft.AnalysisServices Namespace](https://msdn.microsoft.com/library/ms146720\(SQL.130\).aspx) para obtener más información.  
  
> [!NOTE]  
>  Las bibliotecas de cliente de Analysis Services Management Objects (AMO), ADOMD.NET y el modelo de objeto Tabular (TOM) ahora orientados al runtime de .NET 4.0.   
  
## <a name="see-also"></a>Vea también  
 [Guía del desarrollador (Analysis Services)](../../analysis-services/analysis-services-developer-documentation.md)   
 [Programación de modelo tabular para la compatibilidad 1050 1103 a través de niveles](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/tabular-model-programming-for-compatibility-levels-1050-through-1103.md)   
 [Referencia técnica de ](../../analysis-services/powershell/technical-reference-ssas.md) [actualizar Analysis Services](../../database-engine/install-windows/upgrade-analysis-services.md)  
 [Niveles de compatibilidad de los modelos tabulares y las bases de datos](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/tabular-model-programming-for-compatibility-levels-1050-through-1103.md)  
  
  
