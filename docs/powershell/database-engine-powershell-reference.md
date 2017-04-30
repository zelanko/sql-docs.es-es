---
title: Referencia del motor de base de datos de PowerShell | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3c379a43-c497-47dd-8e7d-2b015c068bb7
caps.latest.revision: 8
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: dc3df1d697b05201ac48520c1e344c28648cdfaf
ms.lasthandoff: 04/11/2017

---
# <a name="database-engine-powershell-reference"></a>Referencia del motor de base de datos de PowerShell
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] incluye un conjunto de cmdlets de Windows PowerShell 2.0 para realizar acciones comunes en [!INCLUDE[ssDE](../includes/ssde-md.md)]. Además, las expresiones de consulta y los nombres de recursos uniformes (URN) pueden convertirse en rutas acceso de SQL Server PowerShell o usarse para especificar uno o más objetos en [!INCLUDE[ssDE](../includes/ssde-md.md)].  
  
## <a name="database-engine-cmdlets"></a>Cmdlets del motor de base de datos  
 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] incluye relativamente pocos cmdlets para [!INCLUDE[ssDE](../includes/ssde-md.md)]. La mayoría de los scripts de PowerShell que funcionan con [!INCLUDE[ssDE](../includes/ssde-md.md)] usan el proveedor de SQL Server PowerShell y los modelos de objetos de administración. Para más información, consulte [SQL Server PowerShell Provider](../relational-databases/scripting/sql-server-powershell-provider.md).  
  
 Para obtener información sobre cómo obtener ayuda para los cmdlets de SQL Server en un entorno de Windows PowerShell, vea [Get Help SQL Server PowerShell](../relational-databases/scripting/get-help-sql-server-powershell.md).  
  
### <a name="in-this-section"></a>En esta sección  
 Esta sección contiene información sobre los cmdlets.  
  
|Descripción|Cmdlet|  
|-----------------|------------|  
|Ejecuta scripts Transact-SQL y XQuery como los que se pueden ejecutar con la utilidad **sqlcmd** .|[cmdlet Invoke-Sqlcmd](../powershell/invoke-sqlcmd-cmdlet.md)|  
|Evalúa si un objeto de motor de base de datos cumple una directiva de administración basada en directivas.|[cmdlet Invoke-PolicyEvaluation](../powershell/invoke-policyevaluation-cmdlet.md)|  
  
### <a name="information-about-other-cmdlets"></a>Información sobre otros cmdlets  
 Los cmdlets **Encode-Sqlname** y **Decode-Sqlname** le ayudan a especificar los identificadores de SQL Server que contienen caracteres no admitidos en las rutas de acceso de PowerShell. Para más información, consulte [SQL Server Identifiers in PowerShell](../relational-databases/scripting/sql-server-identifiers-in-powershell.md).  
  
 Use el cmdlet **Convert-UrnToPath** para convertir un nombre de recurso único de un objeto de [!INCLUDE[ssDE](../includes/ssde-md.md)] en una ruta de acceso para el proveedor de SQL Server PowerShell. Para más información, consulte [Convert URNs to SQL Server Provider Paths](../relational-databases/scripting/convert-urns-to-sql-server-provider-paths.md).  
  
## <a name="query-expressions-and-unique-resource-names"></a>Expresiones de consulta y nombres de recursos únicos  
 Las expresiones de consulta son cadenas que usan una sintaxis similar a XPath para especificar un conjunto de criterios que enumeran uno o más objetos de una jerarquía del modelo de objetos. Un nombre de recurso único (URN) es un tipo específico de cadena de expresión de consulta que identifica exclusivamente un objeto único. Para más información, consulte [Query Expressions and Uniform Resource Names](../powershell/query-expressions-and-uniform-resource-names.md).  
  
## <a name="see-also"></a>Vea también  
 [SQL Server PowerShell](../relational-databases/scripting/sql-server-powershell.md)  
  
  
