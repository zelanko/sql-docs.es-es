---
title: Referencia del motor de base de datos de PowerShell | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 3c379a43-c497-47dd-8e7d-2b015c068bb7
caps.latest.revision: 7
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 17424e5a629a4161760c35d5dcc24b80aaf9c2bd
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37205845"
---
# <a name="database-engine-powershell-reference"></a>Referencia del motor de base de datos de PowerShell
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] incluye un conjunto de cmdlets de Windows PowerShell 2.0 para realizar acciones comunes en [!INCLUDE[ssDE](../includes/ssde-md.md)]. Además, las expresiones de consulta y los nombres de recursos uniformes (URN) pueden convertirse en rutas acceso de SQL Server PowerShell o usarse para especificar uno o más objetos en [!INCLUDE[ssDE](../includes/ssde-md.md)].  
  
## <a name="database-engine-cmdlets"></a>Cmdlets del motor de base de datos  
 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] incluye relativamente pocos cmdlets para [!INCLUDE[ssDE](../includes/ssde-md.md)]. La mayoría de los scripts de PowerShell que funcionan con [!INCLUDE[ssDE](../includes/ssde-md.md)] usan el proveedor de SQL Server PowerShell y los modelos de objetos de administración. Para más información, consulte [SQL Server PowerShell Provider](../powershell/sql-server-powershell-provider.md).  
  
 Para obtener información sobre cómo obtener ayuda para los cmdlets de SQL Server en un entorno de Windows PowerShell, vea [Get Help SQL Server PowerShell](../powershell/sql-server-powershell.md).  
  
### <a name="in-this-section"></a>En esta sección  
 Esta sección contiene información sobre los cmdlets.  
  
|Descripción|Cmdlet|  
|-----------------|------------|  
|Ejecuta scripts de Transact-SQL y XQuery, como secuencias de comandos que se pueden ejecutar con la `sqlcmd` utilidad.|[Cmdlet Invoke-Sqlcmd](../../2014/database-engine/invoke-sqlcmd-cmdlet.md)|  
|Evalúa si un objeto de motor de base de datos cumple una directiva de administración basada en directivas.|[Cmdlet Invoke-PolicyEvaluation](../../2014/database-engine/invoke-policyevaluation-cmdlet.md)|  
  
### <a name="information-about-other-cmdlets"></a>Información sobre otros cmdlets  
 El `Encode-Sqlname` y `Decode-Sqlname` cmdlets le ayudan a especificar los identificadores de SQL Server que contienen caracteres no admitidos en las rutas de PowerShell. Para más información, consulte [SQL Server Identifiers in PowerShell](../powershell/sql-server-identifiers-in-powershell.md).  
  
 Use el cmdlet `Convert-UrnToPath` para convertir un nombre de recurso único de un objeto de [!INCLUDE[ssDE](../includes/ssde-md.md)] en una ruta de acceso para el proveedor de SQL Server PowerShell. Para más información, consulte [Convert URNs to SQL Server Provider Paths](../../2014/database-engine/convert-urns-to-sql-server-provider-paths.md).  
  
## <a name="query-expressions-and-unique-resource-names"></a>Expresiones de consulta y nombres de recursos únicos  
 Las expresiones de consulta son cadenas que usan una sintaxis similar a XPath para especificar un conjunto de criterios que enumeran uno o más objetos de una jerarquía del modelo de objetos. Un nombre de recurso único (URN) es un tipo específico de cadena de expresión de consulta que identifica exclusivamente un objeto único. Para más información, consulte [Query Expressions and Uniform Resource Names](../powershell/query-expressions-and-uniform-resource-names.md).  
  
## <a name="see-also"></a>Vea también  
 [SQL Server PowerShell](../powershell/sql-server-powershell.md)  
  
  
