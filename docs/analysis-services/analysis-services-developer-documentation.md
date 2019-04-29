---
title: Documentación para desarrolladores de Analysis Services | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8822a85e39efde36a04b92e8a926adca6839cf58
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62930325"
---
# <a name="analysis-services-developer-documentation"></a>Documentación para desarrolladores de Analysis Services
[!INCLUDE[ssas-appliesto-sqlas-aas](../includes/ssas-appliesto-sqlas-aas.md)]

En Analysis Services, prácticamente cualquier carga de trabajo y el objeto son programable y, a menudo hay más de un método para elegir.  Las opciones incluyen escribir código administrado, secuencias de comandos o mediante unos estándares abiertos como XMLA y MSOLAP si los requisitos de la solución impiden mediante .NET framework.

## <a name="what-you-can-accomplish-in-code"></a>Lo que se puede lograr en código
Escenarios de programación habituales incluyen servidor e implementación de la base de datos, administración, modelo y creación de la base de datos y acceso a datos desde sus aplicaciones personalizadas y los informes que utilizan datos de Analysis Services. Comunes a todos estos escenarios es una fijo arquitectura y el objeto de definición jerarquía, con las operaciones bien definidas que abarcan la definición de datos, procesamiento y cargas de trabajo de consulta.

Aunque los objetos y las cargas de trabajo son programables, no son extensibles. En concreto, no se puede crear los cartuchos de datos personalizados que recuperar datos de orígenes de datos no admitido, personalizan o reemplazar los comportamientos de motor de fórmula o almacenamiento, ni puede crear nuevos tipos de metadatos de objetos en un servidor, la base de datos o el modelo.

Para ampliar aún más el último punto sobre la creación de nuevos tipos de objetos: mientras no se puede crear un nuevo tipo de objeto, puede crear los objetos calculados que se crea a partir de expresiones o código en tiempo de ejecución. No todo el contenido del modelo debe predefinidos y asignado a una estructura de datos existente. Además, puede ampliar el esquema a través de las anotaciones en AMO para pasar información específica del objeto a la aplicación cliente.

## <a name="choose-a-platform-or-approach-to-development"></a>Elija una plataforma o el enfoque de desarrollo
Analysis Services proporciona muchas formas de personalizar una solución a través del código, pero la mayoría de los desarrolladores usa la API administrada o el script.

- Las API administradas incluyen [AMO y TOM](http://msdn.microsoft.com/library/mt436122.aspx) para la definición de datos y las tareas administrativas, y [ADOMD.NET](http://msdn.microsoft.com/library/mt465769.aspx) para poder realizar consultas desde el código de cliente. En SQL Server 2016, AMO se actualiza para usar los nuevos metadatos tabulares para los modelos creados o actualizados en el nivel de compatibilidad 1200 y superior.

- Secuencia de comandos a menudo puede lograr los mismos resultados que un programa ejecutable, con posiblemente menos trabajo.

  - Puede escribir el script de PowerShell con los componentes de Analysis Services PowerShell que llaman directamente a los tipos AMO. En PowerShell, también puede crear y ejecutar ASSL/XMLA o un script TMSL (en JSON).

  - ASSL y TMSL son lenguajes de secuencias de comandos que proporcionan los objetos que se utilizan en detección y ejecutan las operaciones. Depende de qué tipo de secuencia de comandos que usa en el servidor, la base de datos o el modelo subyacente.

  - Los modelos tabulares o bases de datos en el nivel de compatibilidad 1200 y versiones posterior utilizan la Tabular Model Scripting Language (TMSL), que se encuentra en JSON.

  - Los modelos multidimensionales y modelos tabulares en niveles de compatibilidad 1050-1103 usan Analysis Services Scripting Language (ASSL), que es la extensión de estándar abierto XMLA de Analysis Services.

  - Puede generar el script ASSL o TMSL en Management Studio. También puede usar **ver código** en SQL Server Data Tools para ver la definición del modelo de ASSL o TMSL.

- Aunque es posible crear una solución basada en estándares abiertos de MDX y XMLA, es bastante raro que lo haga. No hay ninguna documentación que no sea de XMLA y referencia MDX para ayudarle a usted y la mayoría foro de soporte técnico y Comunidad dibuja de experiencias con .NET o las tecnologías nativas (MSOLAP).

## <a name="programming-in-analysis-services"></a>Programación de Analysis Services
[Programación de minería de datos](../analysis-services/data-mining-programming.md) describe los métodos para compilar soluciones que incluyen objetos de minería de datos.

[Programación de modelos multidimensionales](../analysis-services/multidimensional-models/multidimensional-model-programming.md) describe las tareas de desarrollo y los enfoques para integrar objetos del modelo multidimensional en una solución personalizada.

[Programación de modelos tabulares de nivel de compatibilidad 1200 y superior](../analysis-services/tabular-model-programming-compatibility-level-1200/tabular-model-programming-for-compatibility-level-1200.md)
**nuevo en SQL Server 2016**.  Resume las interfaces y lenguajes de secuencias de comandos que se usan para trabajar con modelos superior y Tabular 1200 mediante programación.

[Programación de modelos tabulares para los niveles de compatibilidad 1050 a 1103](../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/tabular-model-programming-for-compatibility-levels-1050-through-1103.md) esta documentación está dirigida a los desarrolladores que admite modelos tabulares en niveles de compatibilidad menores. Describe las extensiones de CSDL que definen un modelo tabular en la sintaxis XML. También incluye información sobre la sintaxis y las definiciones de modelo de objetos tabulares.

[Objetos de administración de servicios de análisis (AMO)](https://msdn.microsoft.com/library/mt436122.aspx) documentación de referencia para desarrolladores del proveedor administrado, Analysis Services Management Objects (AMO) para la definición de datos y administración, incluido el procesamiento.

[ADOMD.NET](http://msdn.microsoft.com/library/mt465769.aspx) documentación de referencia para desarrolladores del proveedor administrado, ADOMD.NET, que usa para los datos mediante programación las cargas de trabajo de acceso y la consulta.

[Los conjuntos de filas de esquema de Analysis Services](https://docs.microsoft.com/bi-reference/schema-rowsets/analysis-services-schema-rowsets) describe los conjuntos de filas de esquema que proporcionan información sobre el estado del servidor, las operaciones del servidor y objetos de base de datos.

[XML for Analysis &#40;XMLA&#41; referencia](https://docs.microsoft.com/bi-reference/xmla/xml-for-analysis-xmla-reference) conceptos de XMLA describe que pueden ayudarle a entender cómo contribuye XMLA a una solución personalizada. También describe el nivel de cumplimiento de la especificación XMLA 1.1.

[Analysis Services Scripting Language &#40;ASSL para XMLA&#41; ](https://docs.microsoft.com/bi-reference/assl/analysis-services-scripting-language-assl-for-xmla) describe las extensiones ASSL para XMLA. ASSL ofrece un lenguaje de definición y manipulación de datos para modelos multidimensionales de Analysis Services que complementa la especificación XMLA.

[Tabular Model Scripting Language &#40;TMSL&#41; referencia](https://docs.microsoft.com/bi-reference/tmsl/tabular-model-scripting-language-tmsl-reference) TMSL es una representación JSON de los modelos tabulares en el nivel de compatibilidad 1200 y superior. Las definiciones de objeto se basan en construcciones de metadatos tabulares como tabla, columna y relación en lugar de los metadatos multidimensionales que podrían no esté familiarizado si está familiarizado con modelado de datos de Analysis Services en modo Tabular.

[Analysis Services PowerShell Reference](../analysis-services/powershell/analysis-services-powershell-reference.md) se documentan los cmdlets usados para las funciones administrativas, más el uso general **Invoke-ASCmd** cmdlet que acepte cualquier script o una consulta como entrada.

## <a name="see-also"></a>Vea también
[Referencia técnica](../analysis-services/powershell/technical-reference-ssas.md)
[referencia del lenguaje de expresiones y consultas &#40;Analysis Services&#41;](http://msdn.microsoft.com/library/gg492188.aspx)
