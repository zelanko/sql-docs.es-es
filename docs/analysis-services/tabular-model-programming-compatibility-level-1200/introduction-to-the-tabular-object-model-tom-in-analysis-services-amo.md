---
title: "Introducción al modelo de objetos tabulares (TOM) de Analysis Services AMO | Documentos de Microsoft"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 57a4a934-ecd0-4365-8147-d36899d86751
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: a6aeda8e785fcaabef253a8256b5f6f7a842a324
ms.openlocfilehash: 2f9e5d07831070ad69ccf23a3975fbdc19fa4c83
ms.contentlocale: es-es
ms.lasthandoff: 09/21/2017

---
# <a name="introduction-to-the-tabular-object-model-tom-in-analysis-services-amo"></a>Introducción al modelo de objetos Tabular (TOM) en Analysis Services AMO

[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

  El modelo de objetos tabulares (TOM) es una extensión de la biblioteca de cliente de objeto de administración de servicios de análisis (AMO), creada para admitir escenarios de programación para los modelos tabulares que se integró en el nivel de compatibilidad 1200 y versiones posterior. Al igual que con AMO, TOM ofrece un mecanismo de programación para controlar funciones administrativas como la creación de modelos, importar y actualizar los datos y asignación de roles y permisos.  
  
TOM expone metadatos tabulares nativo, como **modelo**, **tablas**, **columnas**, y **relaciones** objetos.  Una vista de alto nivel del árbol de modelo de objetos, que se proporciona a continuación, muestra cómo se relacionan los componentes.  
  
 Dado que TOM es una extensión de AMO, todas las clases que representan los nuevos objetos tabulares introducidos en SQL Server 2016 se implementan en un nuevo ensamblado Microsoft.AnalysisServices.Tabular.dll. Clases de propósito general de AMO se han movido al ensamblado Microsoft.AnalysisServices.Core. El código necesitará hacer referencia a ambos ensamblados.
Vea [instalar, distribuir y hacer referencia al modelo de objetos tabulares &#40; Microsoft.AnalysisServices.Tabular &#41; ](../../analysis-services/tabular-model-programming-compatibility-level-1200/install-distribute-and-reference-the-tabular-object-model.md) para obtener más información.  
  
 Actualmente, la API está disponible únicamente para el código administrado a través de .NET framework. Para revisar la lista completa de programación opciones, incluida la compatibilidad con lenguaje de secuencia de comandos y consultas, vea [Tabular de modelo de programación para 1200 de nivel de compatibilidad](../../analysis-services/tabular-model-programming-compatibility-level-1200/tabular-model-programming-for-compatibility-level-1200.md).  
  
## <a name="tabular-object-model-hierarchy"></a>Jerarquía del modelo de objetos tabulares  
 Desde una perspectiva lógica, todos los objetos tabulares forman un árbol, la raíz de los cuales es un **modelo**, desciende de base de datos. **Servidor** y **base de datos** no se consideran "tabular" ya que estos objetos también pueden representar una base de datos Multidimensional hospedada en un servidor que se está ejecutando en modo Multidimensional o un modelo Tabular con una compatibilidad inferior nivel que no usa metadatos tabulares para definiciones de objeto. 
  
 Con la excepción de **AttributeHierarchy**, **KPI**, y **LinguisticMetadata**, cada objeto secundario puede ser un miembro de una colección. Por ejemplo, el **modelo** objeto contiene una colección de **tabla** objetos (a través de la **tablas** propiedad), con cada **tabla** objeto que contiene una colección de **columna** objetos y así sucesivamente.  
  
 El descendiente de nivel más bajo de cualquier objeto primario de esta jerarquía es una **anotación** objeto que puede utilizarse desea ampliar el esquema como proporcionar el código para controlarla.  
  
 ![diagrama de jerarquía de objetos](../../analysis-services/tabular-model-programming-compatibility-level-1200/media/ssastomobjectmodeldiagram.png "diagrama de jerarquía de objetos")  
  
## <a name="tom-and-other-related-technologies"></a>TOM y otras tecnologías relacionadas

TOM se basa en la infraestructura AMO, que incorpora también Multidimensional y Tabular bases de datos en niveles de compatibilidad inferior a 1200.

Esto tiene algunas implicaciones resulta muy prácticos.
Primer lugar, cuando se administran los objetos que no se especifican en los metadatos tabulares (como un **Server** o **base de datos**), debe aprovechar partes de la pila AMO existente que describen esos objetos. Junto con la API heredada es el concepto de objetos principales y secundarios que proporcionan descripciones granular de estado del objeto como detectado desde el servidor, o cuando se guarda en el servidor. La clase de elemento MajorObject en el espacio de nombres de Microsoft.AnalysisServices expone métodos para **actualizar** y **actualización**. Los objetos secundarios son única actualización o guardar a través del objeto principal que los contiene.

En cambio, cuando se administran los objetos que forman parte de los metadatos tabulares (como **modelo** o **tabla**), que aproveche una pila Tabular completamente nueva. En esta pila, las actualizaciones son específicas, lo que significa cada objeto de metadatos (derivado de la **MetadataObject** clase en el espacio de nombres Microsoft.AnalysisServices.Tabular) pueden guardarse por separado en el servidor. Por lo general, debería detectar toda la **modelo**, a continuación, realizar cambios en objetos de metadatos individuales en él (como **tabla** o **columna**), a continuación, llamar a ** Model.SaveChanges()** método (que entiende los cambios realizados por el usuario en un nivel específico), enviar comandos al servidor para actualizar solo los objetos que ha cambiado.

### <a name="tom-and-xmla"></a>TOM y XMLA

En la conexión, TOM usa el protocolo XMLA para comunicarse con el servidor de Analysis Services y para administrar los objetos. Al administrar los objetos no tabulares, TOM usa [ASSL](/sql-docs/docs/analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla), la extensión de Analysis Services Scripting Language de XMLA. Al administrar los objetos tabulares, TOM usa el protocolo tabular de SSAS, también una extensión de XMLA. Vea [documentación del protocolo MS-SSAS-T SQL Server Analysis Services Tabular](https://msdn.microsoft.com/library/mt719260.aspx) para obtener más información.

### <a name="tom-and-json"></a>TOM y JSON

Los metadatos tabulares, que se estructuran como documentos JSON, tiene una sintaxis nueva de definición modelo comando y el objeto a través de Tabular Model Scripting Language [TMSL](/sql-docs/docs/analysis-services/tabular-model-scripting-language-tmsl-reference). El lenguaje de scripting utiliza JSON para el cuerpo de solicitudes y respuestas.

Aunque TMSL y TOM exponen los mismos objetos (**tabla**, **columna**, etc.) y las mismas operaciones (**crear**, **eliminar**, ** Actualizar**), TOM no usa TMSL en la conexión (usa el protocolo MS-SSAS tabular en su lugar, como se indicó anteriormente).

Como un usuario, puede elegir si desea administrar las bases de datos tabulares a través de la biblioteca de TOM desde su programa de C# o un script de PowerShell o mediante un script de TMSL ejecutadas a través de PowerShell, SQL Server Management Studio (SSMS) o un trabajo del Agente SQL Server.

La decisión de utilizar uno de los dos se remiten a las características de sus requisitos. La biblioteca de TOM proporciona funcionalidad mejorada para aquellos en comparación con TMSL. En concreto, mientras que TMSL solo ofrece operaciones generales en el nivel de base de datos, tabla, partición o rol, TOM permite operaciones mucho más depuradas. Para generar o actualizar los modelos mediante programación, necesitará el alcance total de la API en la biblioteca de TOM.
  
## <a name="see-also"></a>Vea también  
 [Programación de modelo tabular de nivel de compatibilidad 1200](../../analysis-services/tabular-model-programming-compatibility-level-1200/tabular-model-programming-for-compatibility-level-1200.md)   
 [Nivel de compatibilidad para modelos tabulares de Analysis Services](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)  
[Analysis Services PowerShell](../../analysis-services/powershell/analysis-services-powershell-reference.md)
  
