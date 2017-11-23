---
title: "Desarrollar con objetos de administración de análisis (AMO) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- Analysis Management Objects, programming
- AMO, programming
ms.assetid: 91354fc9-22da-4724-b97f-3b1e7b0e69d3
caps.latest.revision: "47"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: bbcf54edc79a1e8254ad6210d327f4a83973f1fd
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
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
[Desarrollar con Analysis Services Scripting Language &#40; ASSL &#41; ](../../../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md) 
 [Desarrollar con XMLA en Analysis Services](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)
