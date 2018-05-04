---
title: Referencia de PowerShell de Analysis Services | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ''
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3876581c0be890870db4d760b41715c36018e25f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="analysis-services-powershell-reference"></a>Referencia de Analysis Services PowerShell
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Cmdlets de PowerShell se incluyen en el [módulo SqlServer](https://www.powershellgallery.com/packages/SqlServer/21.0.17099). 
  
>[!NOTE] 
> Azure operaciones de base de datos de Analysis Services utilizan el mismo módulo de SQL Server como SQL Server Analysis Services. Sin embargo, no todos los cmdlets se admiten para los servicios de análisis de Azure. Para obtener más información, consulte [administrar Azure Analysis Services con PowerShell](https://docs.microsoft.com/azure/analysis-services/analysis-services-powershell).
  
##  <a name="bkmk_cmdlets"></a> Cmdlets de Analysis Services  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] proporciona cmdlets que se corresponden con métodos en el espacio de nombres **Microsoft.AnalysisServices** . La tabla siguiente describe cada cmdlet y proporciona un vínculo al método AMO correspondiente.  
  
 Si quiere usar PowerShell para realizar una tarea que no está representada en la lista siguiente (por ejemplo, crear o sincronizar una base de datos), puede escribir el script XMLA o TMSL para esa acción y, después, ejecutarla con el cmdlet **Invoke-ASCmd** .  
  
|Cmdlet|Description|Métodos equivalentes de AMO|  
|------------|-----------------|----------------------------|  
|[Cmdlet Add-RoleMember](../../analysis-services/powershell/add-rolemember-cmdlet.md)|Agregar un miembro a un rol de base de datos.|<xref:Microsoft.AnalysisServices.RoleMemberCollection.Add%2A>|  
|[Cmdlet Backup-ASDatabase](../../analysis-services/powershell/backup-asdatabase-cmdlet.md)|Realizar copias de seguridad de una base de datos de Analysis Services.|[Database.Backup](https://msdn.microsoft.com/library/microsoft.analysisservices.database.backup.aspx)|  
|[Cmdlet Invoke-ASCmd](../../analysis-services/powershell/invoke-ascmd-cmdlet.md)|Ejecutar una consulta o un script en formato XMLA o TSML (JSON).|<xref:Microsoft.AnalysisServices.Core.Server.Execute%2A>|  
|[Invoke-ProcessASDatabase](../../analysis-services/powershell/invoke-processasdatabase.md)|Procesar una base de datos.|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Cmdlet Invoke-ProcessCube](../../analysis-services/powershell/invoke-processcube-cmdlet.md)|Procesar un cubo.|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Cmdlet Invoke-ProcessDimension](../../analysis-services/powershell/invoke-processdimension-cmdlet.md)|Procesar una dimensión.|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Cmdlet Invoke-ProcessPartition](../../analysis-services/powershell/invoke-processpartition-cmdlet.md)|Procesar una partición.|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Cmdlet Invoke-ProcessTable](../../analysis-services/powershell/invoke-processtable-cmdlet.md)|Procesar una tabla en un modelo Tabular, un modelo de compatibilidad 1200 o superior.|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Cmdlet Merge-Partition](../../analysis-services/powershell/merge-partition-cmdlet.md)|Combinar una partición.|<xref:Microsoft.AnalysisServices.Partition.Merge%2A>|  
|[Cmdlet New-RestoreFolder](../../analysis-services/powershell/new-restorefolder-cmdlet.md)|Crear una carpeta que contenga una copia de seguridad de la base de datos.|<xref:Microsoft.AnalysisServices.RestoreFolder>|  
|[Cmdlet New-RestoreLocation](../../analysis-services/powershell/new-restorelocation-cmdlet.md)|Especificar uno o varios servidores remotos en los que restaurar la base de datos.|<xref:Microsoft.AnalysisServices.RestoreLocation>|  
|[Cmdlet Remove-RoleMember](../../analysis-services/powershell/remove-rolemember-cmdlet.md)|Quitar un miembro de un rol de base de datos.|<xref:Microsoft.AnalysisServices.RoleMemberCollection.Remove%2A>|  
|[Cmdlet Restore-ASDatabase](../../analysis-services/powershell/restore-asdatabase-cmdlet.md)|Restaurar una base de datos en una instancia de servidor.|<xref:Microsoft.AnalysisServices.Core.Server.Restore%2A>|  
  

  
  
