---
title: Desarrollar con objetos de administración de análisis (AMO) | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: amo
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6f47c7fe9abc3b7a23c0eea2dd78a536fb9e0ad2
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
ms.locfileid: "34027575"
---
# <a name="developing-with-analysis-management-objects-amo"></a>Desarrollar con Objetos de administración de análisis (AMO)
Analysis Management Objects (AMO) es la biblioteca completa de objetos que se accede mediante programación que permite a una aplicación administrar una instancia en ejecución de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].

En esta sección se explican los conceptos de AMO, centrándose en los objetos principales, cómo y cuándo utilizarlos y la forma en que se interrelacionan. Para obtener más información acerca de determinados objetos o clases, vea:

- [Namespace Microsoft.AnalysisServices](http://msdn.microsoft.com/library/microsoft.analysisservices.aspx), documentación de referencia
- [Objetos de administración de servicios de análisis (AMO)](http://www.bing.com/search?q=Analysis+Services+Management+Objects+%28AMO%29), como una búsqueda general Bing.com.


 **Novedades en SQL Server 2016**

En SQL Server 2016, AMO se ha refactorizado en varios ensamblados. Las clases genéricas, como el servidor, base de datos y funciones están en el **Microsoft.AnalysisServices.Core** Namespace. Las API específicas de multidimensional permanecen en [Microsoft.AnalysisServices Namespace](https://msdn.microsoft.com/library/ms146720.aspx).

Secuencias de comandos personalizadas y las aplicaciones escritas para versiones anteriores de AMO seguirán funcionando sin modificaciones. Sin embargo, si tiene secuencias de comandos o aplicaciones que tienen como destino SQL Server 2016 en concreto, o si necesita volver a generar una solución personalizada, asegúrese de agregar el nuevo ensamblado y el espacio de nombres para el proyecto.

## <a name="see-also"></a>Vea también
[Desarrollar aplicaciones con Analysis Services Scripting Language &#40;ASSL&#41;](../../../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)
[desarrollar con XMLA en Analysis Services](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)
