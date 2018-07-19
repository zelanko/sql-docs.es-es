---
title: Información general sobre extensibilidad para reglas de análisis de código de base de datos | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- SQL Server 2014
- SQL Server 2016 Preview
ms.assetid: 62f5c980-18d5-43fe-b443-c9e149d01fc7
caps.latest.revision: 9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 573ca1357b205f31b2bce54a39a46fb95acece0e
ms.sourcegitcommit: 2f07d285824a8982c279f3816b220e61a2d91b06
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/29/2018
ms.locfileid: "37094622"
---
# <a name="overview-of-extensibility-for-database-code-analysis-rules"></a>Información general sobre extensibilidad para reglas de análisis de código de base de datos
Las ediciones de Visual Studio que contienen SQL Server Data Tools incluyen reglas de análisis de código que proporcionan información acerca del diseño, nomenclatura y advertencias de rendimiento de Transact\-SQL en el código de la base de datos. Para obtener más información, consulte [Análisis del código de bases de datos para mejorar la calidad del código](http://msdn.microsoft.com/en-us/library/dd172133(v=vs.100).aspx).  
  
Si las reglas de análisis de código integradas no abarcan un problema de Transact\-SQL determinado que desee incluir, puede crear reglas de análisis de código de base de datos personalizadas. Por ejemplo, es posible que desee crear una regla personalizada que evite el uso de la instrucción WAITFOR DELAY, como se demuestra en [Walkthrough Authoring a Custom Static Code Analysis Rule Assembly for SQL Server](../ssdt/walkthrough-author-custom-static-code-analysis-rule-assembly.md). (Tutorial para la creación de un ensamblado de reglas de análisis de código estático personalizadas para SQL Server). Para crear reglas de análisis de código de base de datos personalizadas, utilice las clases del espacio de nombres [CodeAnalysis](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.codeanalysis.aspx).  
  
Antes de crear reglas de análisis de código personalizadas, deberá comprender la arquitectura básica de los distintos componentes de las reglas de análisis de código de base de datos.  
  
## <a name="database-code-analysis-rules-components"></a>Componentes de las reglas de análisis de código de base de datos  
En el siguiente diagrama se muestra cómo interactúan los componentes de las reglas de análisis de código de base de datos:  
  
![Componentes de las reglas de análisis de código de base de datos](../ssdt/media/ssdt-database-code-analysis-rules-components.jpg "Database Code Analysis Rules Components")  
  
Cuando se usa la característica de análisis de código de base de datos, ya sea mediante la ejecución directa de análisis de código estático (para obtener más información, consulte [Cómo: analizar código de Transact-SQL para buscar defectos](http://msdn.microsoft.com/en-us/library/dd172119(v=vs.100).aspx)) o mediante la realización de una compilación, todas las reglas se cargan y utilizan según cómo se hayan configurado en el proyecto. Para obtener más información, consulte [Cómo: habilitar y deshabilitar reglas específicas para el análisis de código estático de base de datos](http://msdn.microsoft.com/en-us/library/dd172131(v=vs.100).aspx). El Administrador de extensiones también cargará los ensamblados de reglas personalizadas que haya creado y registrado. Para obtener más información, consulte [Cómo: instalar y administrar las extensiones de características](../ssdt/how-to-install-and-manage-feature-extensions.md).  
  
Una clase de reglas de análisis de código personalizadas hereda de [SqlCodeAnalysisRule](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.codeanalysis.sqlcodeanalysisrule.aspx). La clase de reglas personalizadas puede tener acceso a un número de objetos útiles a través de su contexto de ejecución de regla. Estos incluyen:  
  
-   Metadatos acerca de la propia regla.  
  
-   El Dac.Model.TSqlModel que representa el esquema de la base de datos, incluidos todos los elementos del modelo, las relaciones entre estos y las propiedades de los elementos.  
  
-   Para las reglas que examinan elementos específicos, se incluye en el contexto el Dac.Model.TSqlObject que representa ese elemento del esquema en el modelo.  
  
-   Muchos de los objetos de esquema también tienen una representación [ScriptDom](https://msdn.microsoft.com/en-us/library/microsoft.sqlserver.transactsql.scriptdom.aspx) a la que se puede acceder a través de este contexto. Se trata de una representación basada en el AST de un elemento que puede ser útil cuando se intentan detectar posibles problemas de sintaxis, como la presencia de [SelectStarExpression](https://msdn.microsoft.com/en-us/library/microsoft.sqlserver.transactsql.scriptdom.selectstarexpression.aspx).  
  
La regla crea un Dac.CodeAnalysis.SqlRuleProblem para representar los problemas encontrados por esta. Al crearla, el Dac.Model.TSqlObject pertinente y posiblemente un elemento de representación [ScriptDom](https://msdn.microsoft.com/en-us/library/microsoft.sqlserver.transactsql.scriptdom.aspx) se pasan al constructor y se utilizan para determinar la ubicación del problema en los archivos de código fuente. Al final del análisis, todos estos problemas se pasan al Administrador de errores y se muestran en la lista de errores.  
  
## <a name="see-also"></a>Ver también  
[Extensión de las características de base de datos](../ssdt/extending-the-database-features.md)  
  
