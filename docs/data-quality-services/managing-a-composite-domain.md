---
title: Administrar un dominio compuesto
ms.date: 07/31/2012
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 47821eff-800b-4053-8d36-e42bbc267f54
author: swinarko
ms.author: sawinark
ms.openlocfilehash: ae41076d014e86e0f37978cfa72a49f0d3002959
ms.sourcegitcommit: 6be9a0ff0717f412ece7f8ede07ef01f66ea2061
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85814082"
---
# <a name="managing-a-composite-domain"></a>Administrar un dominio compuesto

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  En este tema se describe el uso de los dominios compuestos en [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). En ocasiones, un dominio individual no representa los datos de un campo de forma satisfactoria, y estos solo se pueden representar agrupando varios dominios individuales. Para ello, es necesario crear un dominio compuesto. Un dominio compuesto consta de dos o más dominios individuales y se asigna a un campo de datos que consta de varios términos relacionados que no están analizados, sino que se incluyen en un valor compuesto único. Cada término de dicho valor se representará mediante un dominio individual distinto. Una vez que se han incluido dominios individuales en dominios compuestos y se ha asignado el dominio compuesto al campo de datos, es posible generar conocimiento en la base de conocimiento sobre los datos de dicho campo generando conocimiento en los dominios individuales. Un dominio compuesto, al igual que un dominio individual, es una representación semántica de los datos de un solo campo de datos.  
  
 Los dominios individuales de un dominio compuesto deben tener un área común de conocimiento. Un ejemplo es un campo de dirección que incluye datos sobre la calle, la ciudad, el estado, el país y el código postal. Los distintos términos de este campo podrían tener tipos de datos diferentes. Para ocuparse de esto, es necesario asignar dichos términos a dominios individuales diferentes. Otro ejemplo es un campo de nombre completo que contiene el nombre, las iniciales y los apellidos. Para utilizar un dominio compuesto, es necesario analizar los datos del campo en distintos dominios individuales, creando un dominio compuesto para el campo y un dominio individual para cada parte del campo.  
  
 Los dominios compuestos no tienen las mismas capacidades que los dominios individuales. No es posible cambiar los valores en el dominio compuesto; esta operación se debe realizar en un dominio individual. Es posible utilizar reglas entre dominios para probar los valores de los dominios individuales del dominio compuesto. También se pueden ver las combinaciones de valores encontradas en los dominios compuestos.  
  
## <a name="in-this-section"></a>En esta sección  
 El uso de un dominio compuesto le permite hacer lo siguiente:  
  
|||  
|-|-|  
|Crear una representación semántica de un campo de datos que consta de varios términos relacionados que no se analizan|[Crear un dominio compuesto](../data-quality-services/create-a-composite-domain.md)|  
|Cuando se asignan datos complejos a un dominio compuesto, dichos datos se pueden analizar basándose tanto en el conocimiento como en un delimitador. DQS intentará primero utilizar su conocimiento sobre los dominios individuales para determinar la pertenencia de las partes de la cadena compleja a dichos dominios.|[Crear un dominio compuesto](../data-quality-services/create-a-composite-domain.md)|  
|Adjuntar un servicio de datos de referencia, como un servicio que administre los datos de direcciones, a un dominio compuesto.|[Adjuntar un dominio o un dominio compuesto a datos de referencia](../data-quality-services/attach-domain-or-composite-domain-to-reference-data.md)|  
|Crear una regla entre dominios cuando el valor de un dominio individual de un dominio compuesto afecta al valor de otro.|[Crear una regla entre dominios](../data-quality-services/create-a-cross-domain-rule.md)|  
|Identificar combinaciones de valores para que DQS pueda informar sobre su frecuencia.|[Utilizar relaciones de valor en un dominio compuesto](../data-quality-services/use-value-relations-in-a-composite-domain.md)|  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descripción de la tarea|Tema|  
|----------------------|-----------|  
|Generar una base de conocimiento ejecutando la detección de conocimiento y administrando el conocimiento de forma interactiva|[Crear una base de conocimiento](../data-quality-services/building-a-knowledge-base.md)|  
|Importar conocimiento en una base de conocimiento o exportarlo desde esta.|[Importar y exportar conocimiento](../data-quality-services/importing-and-exporting-knowledge.md)|  
|Crear un dominio individual y agregarle conocimiento.|[Administrar un dominio](../data-quality-services/managing-a-domain.md)|  
  
  
