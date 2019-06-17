---
title: Referencia de PowerShell de Analysis Services | Microsoft Docs
ms.date: 06/25/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: powershell
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 13ea15a23bbf6de6c50b494f709f65cae2f7c48b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62509847"
---
# <a name="analysis-services-powershell-reference"></a>Referencia de Analysis Services PowerShell
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Cmdlets de PowerShell se incluyen en el [módulo SqlServer](https://www.powershellgallery.com/packages/SqlServer/21.0.17099). 
  
>[!NOTE] 
> Operaciones de base de datos de Azure Analysis Services use el mismo módulo de SqlServer como SQL Server Analysis Services. Sin embargo, no todos los cmdlets son compatibles con Azure Analysis Services. Para obtener más información, consulte [administrar Azure Analysis Services con PowerShell](https://docs.microsoft.com/azure/analysis-services/analysis-services-powershell).
  
##  <a name="bkmk_cmdlets"></a> Cmdlets de Analysis Services  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] proporciona cmdlets que se corresponden con métodos en el espacio de nombres **Microsoft.AnalysisServices** . La tabla siguiente describe cada cmdlet y proporciona un vínculo al método AMO correspondiente.  
  
 Si quiere usar PowerShell para realizar una tarea que no está representada en la lista siguiente (por ejemplo, crear o sincronizar una base de datos), puede escribir el script XMLA o TMSL para esa acción y, después, ejecutarla con el cmdlet **Invoke-ASCmd** .  
  
|Cmdlet|Descripción|Métodos equivalentes de AMO|  
|------------|-----------------|----------------------------|  
|[Cmdlet Add-RoleMember](https://docs.microsoft.com/powershell/module/sqlserver/Add-RoleMember)|Agregar un miembro a un rol de base de datos.|<xref:Microsoft.AnalysisServices.RoleMemberCollection.Add%2A>|  
|[Cmdlet Backup-ASDatabase](https://docs.microsoft.com/powershell/module/sqlserver/backup-asdatabase)|Realizar copias de seguridad de una base de datos de Analysis Services.|[Database.Backup](https://msdn.microsoft.com/library/microsoft.analysisservices.database.backup.aspx)|  
|[Cmdlet Invoke-ASCmd](https://docs.microsoft.com/powershell/module/sqlserver/invoke-ascmd)|Ejecutar una consulta o un script en formato XMLA o TSML (JSON).|<xref:Microsoft.AnalysisServices.Core.Server.Execute%2A>|  
|[Invoke-ProcessASDatabase](https://docs.microsoft.com/powershell/module/sqlserver/invoke-processasdatabase)|Procesar una base de datos.|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Cmdlet Invoke-ProcessCube](https://docs.microsoft.com/powershell/module/sqlserver/invoke-processcube)|Procesar un cubo.|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Cmdlet Invoke-ProcessDimension](https://docs.microsoft.com/powershell/module/sqlserver/invoke-processdimension)|Procesar una dimensión.|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Cmdlet Invoke-ProcessPartition](https://docs.microsoft.com/powershell/module/sqlserver/invoke-processpartition)|Procesar una partición.|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Cmdlet Invoke-ProcessTable](https://docs.microsoft.com/powershell/module/sqlserver/invoke-processtable)|Procesar una tabla en un modelo Tabular, el modelo de compatibilidad 1200 o superior.|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Cmdlet Merge-Partition](https://docs.microsoft.com/powershell/module/sqlserver/merge-partition)|Combinar una partición.|<xref:Microsoft.AnalysisServices.Partition.Merge%2A>|  
|[Cmdlet New-RestoreFolder](https://docs.microsoft.com/powershell/module/sqlserver/new-restorefolder)|Crear una carpeta que contenga una copia de seguridad de la base de datos.|<xref:Microsoft.AnalysisServices.RestoreFolder>|  
|[Cmdlet New-RestoreLocation](https://docs.microsoft.com/powershell/module/sqlserver/new-restorelocation)|Especificar uno o varios servidores remotos en los que restaurar la base de datos.|<xref:Microsoft.AnalysisServices.RestoreLocation>|  
|[Cmdlet Remove-RoleMember](https://docs.microsoft.com/powershell/module/sqlserver/remove-rolemember)|Quitar un miembro de un rol de base de datos.|<xref:Microsoft.AnalysisServices.RoleMemberCollection.Remove%2A>|  
|[Cmdlet Restore-ASDatabase](https://docs.microsoft.com/powershell/module/sqlserver/restore-asdatabase)|Restaurar una base de datos en una instancia de servidor.|<xref:Microsoft.AnalysisServices.Core.Server.Restore%2A>|  
  

  
  
