---
description: Limpiar datos en un dominio compuesto
title: Limpiar datos en un dominio compuesto
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 7d1076e0-7710-469a-9107-e293e4bd80ac
author: swinarko
ms.author: sawinark
ms.openlocfilehash: f35430d590be36bb7ae487d32a9a0fc97c0275ce
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449957"
---
# <a name="cleanse-data-in-a-composite-domain"></a>Limpiar datos en un dominio compuesto

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sqlserver.md)]

  Este tema proporciona información sobre la limpieza de dominios compuestos en [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). Un dominio compuesto consta de dos o más dominios individuales y se asigna a un campo de datos que consta de varios términos relacionados. Todos los dominios que forman un dominio compuesto deben tener un área de conocimiento común. Para obtener información detallada acerca de los dominios compuestos, vea [Managing a Composite Domain](../data-quality-services/managing-a-composite-domain.md).  
  
##  <a name="mapping-a-composite-domain-to-the-source-data"></a><a name="Mapping"></a> Asignación de un dominio compuesto a los datos de origen  
 Existen dos formas de asignar los datos de origen a un dominio compuesto:  
  
-   Los datos de origen están en un único campo (por ejemplo, Nombre completo), que está asignado a un dominio compuesto.  
  
    -   Si el dominio compuesto está asignado a un servicio de datos de referencia, los datos de origen se enviarán tal como están a dicho servicio para su corrección y análisis.  
  
    -   Si el dominio compuesto no está asignado a ningún servicio de datos de referencia, los datos de origen se analizarán según el método de análisis definido para el dominio compuesto. Para obtener más información acerca de cómo especificar un método de análisis para los dominios compuestos, vea [Create a Composite Domain](../data-quality-services/create-a-composite-domain.md).  
  
-   Los datos de origen están formados por varios campos (por ejemplo, Nombre, Segundo nombre y Apellidos), que están asignados a los dominios individuales de un dominio compuesto.  
  
 Para ver un ejemplo de cómo asignar dominios compuestos a los datos de origen, vea [Adjuntar un dominio o un dominio compuesto a datos de referencia](../data-quality-services/attach-domain-or-composite-domain-to-reference-data.md).  
  
##  <a name="data-correction-using-definitive-cross-domain-rules"></a><a name="CDCorrection"></a> Corrección de datos mediante reglas entre dominios definitivas  
 Las reglas entre dominios existentes en un dominio compuesto permiten crear reglas que indican la relación que hay entre los dominios que conforman dicho dominio compuesto. Las reglas entre dominios se tienen en cuenta cuando se ejecuta la actividad de limpieza en los datos de origen y resultan involucrados dominios compuestos. Además de permitirle conocer la validez de una regla entre dominios, la cláusula *Then* definitiva **El valor es igual a**de una regla entre dominios también corrige los datos durante la actividad de limpieza de datos.  
  
 Consideremos el siguiente ejemplo: existe un dominio compuesto, Product, con tres dominios individuales: ProductName, CompanyName y ProductVersion. Cree la siguiente regla entre dominios definitiva:  
  
 SI en el dominio "CompanyName" el valor contiene *Microsoft* y en el dominio "ProductName" el valor es igual a *Office* y en "ProductVersion" el valor es igual a *2010* ENTONCES en el dominio "ProductName" el valor es igual a *Microsoft Office 2010*.  
  
 Cuando se ejecuta esta regla entre dominios, los datos de origen (ProductName) se corrigen a los datos siguientes después de la actividad de limpieza:  
  
 **Datos de origen**  
  
|ProductName|CompanyName|ProductVersion|  
|-----------------|-----------------|--------------------|  
|Office|Microsoft Inc.|2010|  
  
 **Datos de salida**  
  
|ProductName|CompanyName|ProductVersion|  
|-----------------|-----------------|--------------------|  
|Microsoft Office 2010|Microsoft Inc.|2010|  
  
 Cuando pruebe la cláusula *Then* definitiva **El valor es igual a**de la regla entre dominios, el cuadro de diálogo **Probar regla de dominio compuesto** contendrá una columna nueva, **Corregir a**, que mostrará los datos correctos. En un proyecto de calidad de datos de limpieza, esta regla entre dominios definitiva cambia los datos con una confianza del 100% y la columna **motivo** muestra el siguiente mensaje: corregido por la regla ' *\<Cross-Domain Rule Name>* '. Para obtener más información acerca de las reglas entre dominios, vea [Create a Cross-Domain Rule](../data-quality-services/create-a-cross-domain-rule.md).  
  
> [!NOTE]  
>  La regla entre dominios definitiva no funcionará en dominios compuestos que estén adjuntados al servicio de datos de referencia.  
  
##  <a name="data-profiling-for-composite-domains"></a><a name="DataProfiling"></a> Generación de perfiles de datos para dominios compuestos  
 El proceso de generación de perfiles de DQS proporciona dos dimensiones de calidad de datos: *integridad* (la medida en que los datos están presentes) y *precisión* (la medida en que los datos se pueden utilizar para su uso previsto) durante la actividad de limpieza. La generación de perfiles no puede proporcionar estadísticas de integridad confiables para los dominios compuestos. Si necesita estadísticas de integridad, utilice dominios individuales en lugar de dominios compuestos. Si desea utilizar dominios compuestos, puede crear una base de conocimiento con dominios individuales para generar los perfiles y determinar la integridad, y crear otro dominio con un dominio compuesto para la actividad de limpieza. Por ejemplo, la generación de perfiles podría mostrar una integridad del 95% para los registros de direcciones utilizando un dominio compuesto, pero podría haber un nivel mucho más alto de falta de integridad en una de las columnas, por ejemplo, una columna de código postal (zip). En este ejemplo, podría medir la integridad de la columna de código postal con un dominio individual.  
  
 La generación de perfiles probablemente proporcione estadísticas precisas y confiables para los dominios compuestos porque permite medir la precisión de varias columnas al mismo tiempo. El valor de estos datos está en la agregación compuesta, por lo que puede ser conveniente medir la precisión con un dominio compuesto.  
  
 Para obtener información detallada sobre la generación de perfiles de datos durante la actividad de limpieza, vea [Estadísticas del generador de perfiles](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md#Profiler) en [Limpiar datos mediante el conocimiento de DQS &#40;interno&#41;](../data-quality-services/cleanse-data-using-dqs-internal-knowledge.md).  
  
  
