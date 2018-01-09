---
title: "Documentación para desarrolladores de Analysis Services | Documentos de Microsoft"
ms.custom: 
ms.date: 03/24/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- multidimensional data [Analysis Services], developer's guide
- developer's guide [Analysis Services - multidimensional data]
ms.assetid: 0a6eda76-1c5e-487e-9c8b-1feb09f1a34c
caps.latest.revision: "22"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 12b3c89ac68cd633c50ea96ded258a91cc066ae8
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="analysis-services-developer-documentation"></a>Documentación para desarrolladores de Analysis Services
[!INCLUDE[ssas-appliesto-sqlas-aas](../includes/ssas-appliesto-sqlas-aas.md)]En Analysis Services, prácticamente cualquier objeto y la carga de trabajo son programable y, a menudo hay más de un enfoque que puede elegir.  Las opciones incluyen escribir código administrado, secuencias de comandos o mediante unos estándares abiertos como XMLA y MSOLAP si los requisitos de la solución impiden mediante .NET framework.

## <a name="what-you-can-accomplish-in-code"></a>¿Qué puede realizar en el código
Escenarios de programación habituales incluyen servidor e implementación de base de datos, administración, modelo y creación de base de datos y acceso a datos desde sus aplicaciones personalizadas e informes que usan datos de Analysis Services. Comunes a todos estos escenarios es una fijo arquitectura y el objeto de definición jerarquía, con las operaciones bien también se entiende que abarcan la definición de datos, el procesamiento y cargas de trabajo de consulta.

Aunque los objetos y las cargas de trabajo son programables, no son extensibles. En concreto, no se puede crear los cartuchos de datos personalizados que recuperar datos de orígenes de datos no admitido, personalizan o reemplazar los comportamientos de motor de fórmula o almacenamiento, ni puede crear nuevos tipos de metadatos del objeto en un servidor, la base de datos o el modelo.

Para obtener más proporcionar información en el último punto sobre la creación de nuevos tipos de objetos: mientras no se puede crear un nuevo tipo de objeto, puede crear objetos calculados que se crea a partir de expresiones o código en tiempo de ejecución. No todos los elementos en el modelo es necesario predefinidos y asignado a una estructura de datos existente. Además, puede extender el esquema a través de las anotaciones de AMO para pasar información específica del objeto a la aplicación cliente.

## <a name="choose-a-platform-or-approach-to-development"></a>Elija una plataforma o el enfoque de desarrollo
Analysis Services proporciona muchas formas de personalizar una solución a través del código, pero la mayoría de los desarrolladores usa la API administrada o el script.

- API administradas que se incluyen [AMO y TOM](http://msdn.microsoft.com/library/mt436122.aspx) de definición de datos y las tareas administrativas, y [ADOMD.NET](http://msdn.microsoft.com/library/mt465769.aspx) para poder realizar consultas desde el código de cliente. En SQL Server 2016, AMO se actualiza para usar los nuevos metadatos tabulares para los modelos creados o actualizados en el nivel de compatibilidad 1200 y versiones posterior.

- Secuencia de comandos a menudo puede lograr los mismos resultados que un programa ejecutable, y posiblemente menos esfuerzo.

  - Puede escribir script de PowerShell con los componentes de Analysis Services PowerShell que llaman directamente a los tipos AMO. En PowerShell, también puede crear y ejecutar ASSL/XMLA o un script de TMSL (en JSON).

  - ASSL y TMSL son lenguajes de secuencias de comandos que proporcionan los objetos que se utilizan en detectarán y ejecutan las operaciones. ¿Qué tipo de secuencia de comandos utilizar depende en el servidor, la base de datos o el modelo subyacente.

  - Los modelos tabulares o las bases de datos en el nivel de compatibilidad 1200 y versiones posterior utilice la Tabular Model Scripting Language (TMSL), que se encuentra en JSON.

  - Modelos multidimensionales como tabulares en niveles de compatibilidad 1050-1103 usar Analysis Services Scripting Language (ASSL), que es la extensión de Analysis Services del estándar abierto XMLA.

  - Puede generar secuencias de comandos ASSL y TMSL en Management Studio. También puede usar **ver código** en SQL Server Data Tools para ver la definición del modelo de ASSL o TMSL.

- Aunque es posible compilar una solución basada en estándares abiertos de MDX y XMLA, es bastante raro que lo haga. No hay ninguna documentación distinto de XMLA y referencia MDX para ayudar a y la mayoría de comunidad y foro admiten dibuja de experiencias con .NET o nativo tecnologías (MSOLAP).

## <a name="programming-in-analysis-services"></a>Programación de Analysis Services
[Programación de minería de datos](../analysis-services/data-mining-programming.md) describe los métodos para compilar soluciones que incluyen objetos de minería de datos.

[Programación de modelo multidimensionales](../analysis-services/multidimensional-models/multidimensional-model-programming.md) describe las tareas de desarrollo y los enfoques para integrar objetos del modelo multidimensional en una solución personalizada.

[Programación de modelo tabulares de 1200 de nivel de compatibilidad y versiones posteriores](../analysis-services/tabular-model-programming-compatibility-level-1200/tabular-model-programming-for-compatibility-level-1200.md)
**nuevo en SQL Server 2016**.  Resume las interfaces y lenguajes de script utilizados para trabajar con modelos superior y Tabular 1200 mediante programación.

[Programación de modelo tabular para 1050 de niveles de compatibilidad a través de 1103](../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/tabular-model-programming-for-compatibility-levels-1050-through-1103.md) esta documentación está destinada a desarrolladores que admitan modelos tabulares en niveles de compatibilidad anterior. Describe las extensiones de CSDL que definen un modelo tabular en la sintaxis XML. También incluye información sobre las definiciones de modelo de objetos tabulares y sintaxis.

[Objetos de administración de servicios de análisis (AMO)](https://msdn.microsoft.com/library/mt436122.aspx) documentación de referencia para desarrolladores del proveedor administrado, Analysis Services Management Objects (AMO) para la definición de datos y administración, incluido el procesamiento.

[ADOMD.NET](http://msdn.microsoft.com/library/mt465769.aspx) documentación de referencia para desarrolladores del proveedor administrado, ADOMD.NET, que usa para los datos mediante programación las cargas de trabajo de acceso y la consulta.

[Conjuntos de filas de esquema de Analysis Services](../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md) describe los conjuntos de filas de esquema que proporcionan información sobre el estado del servidor, las operaciones del servidor y objetos de base de datos.

[XML for Analysis &#40; XMLA &#41; Referencia](../analysis-services/xmla/xml-for-analysis-xmla-reference.md) conceptos de XMLA describe que pueden ayudarle a entender cómo contribuye XMLA a una solución personalizada. También describe el nivel de cumplimiento de la especificación XMLA 1.1.

[Analysis Services Scripting Language &#40; ASSL para XMLA &#41; ](../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md) Describe las extensiones ASSL para XMLA. ASSL ofrece un lenguaje de definición y manipulación de datos para modelos multidimensionales de Analysis Services que complementa la especificación XMLA.

[Tabular Model Scripting Language &#40; TMSL &#41; Referencia](../analysis-services/tabular-model-scripting-language-tmsl-reference.md) TMSL es una representación JSON de los modelos tabulares en el nivel de compatibilidad 1200 y versiones posterior. Las definiciones de objeto se basan en construcciones de metadatos tabulares como tabla, columna y la relación en lugar de metadatos multidimensionales que podrían ser poco familiar si está familiarizado con modelado de datos de Analysis Services en modo Tabular.

[Analysis Services PowerShell Reference](../analysis-services/powershell/analysis-services-powershell-reference.md) documenta los cmdlets usados para las funciones administrativas, junto con el uso general **Invoke-ASCmd** cmdlet que acepte cualquier script o una consulta como entrada.

## <a name="see-also"></a>Vea también
[Referencia técnica de &#40; SSAS &#41; ](../analysis-services/powershell/technical-reference-ssas.md) 
 [y referencia del lenguaje de expresión de consultas &#40; Analysis Services &#41;](http://msdn.microsoft.com/library/gg492188.aspx)
