---
title: "Referencia de Analysis Services PowerShell | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 6c435e40-bfaf-4073-8cef-bc3260602246
caps.latest.revision: 9
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 9
---
# Referencia de Analysis Services PowerShell
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] incluye un proveedor de PowerShell (SQLAS) y cmdlets (SQLASCMDLETS) que permiten usar Windows PowerShell para navegar, administrar y consultar objetos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Para obtener más información sobre la carga y el uso del proveedor y los cmdlets, vea [PowerShell scripting in Analysis Services](../../analysis-services/instances/powershell-scripting-in-analysis-services.md). Para obtener un ejemplo de cómo utilizar los tipos AMO en PowerShell para crear una base de datos tabular, consulte [AMO PowerShell Example](../../analysis-services/powershell/amo-powershell-example.md).  
  
##  <a name="bkmk_cmdlets"></a> Cmdlets de Analysis Services  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] proporciona cmdlets que se corresponden con métodos en el espacio de nombres **Microsoft.AnalysisServices**. La tabla siguiente describe cada cmdlet y proporciona un vínculo al método AMO correspondiente.  
  
 Si quiere usar PowerShell para realizar una tarea que no está representada en la lista siguiente (por ejemplo, crear o sincronizar una base de datos), puede escribir el script XMLA o TMSL para esa acción y, después, ejecutarla con el cmdlet **Invoke-ASCmd**.  
  
|Cmdlet|Description|Métodos equivalentes de AMO|  
|------------|-----------------|----------------------------|  
|[Cmdlet Add-RoleMember](../../analysis-services/powershell/add-rolemember-cmdlet.md)|Agregar un miembro a un rol de base de datos.|<xref:Microsoft.AnalysisServices.RoleMemberCollection.Add%2A>|  
|[Cmdlet Backup-ASDatabase](../../analysis-services/powershell/backup-asdatabase-cmdlet.md)|Realizar copias de seguridad de una base de datos de Analysis Services.|<xref:Microsoft.AnalysisServices.Database.Backup%2A>|  
|[Cmdlet Invoke-ASCmd](../../analysis-services/powershell/invoke-ascmd-cmdlet.md)|Ejecutar una consulta o un script en formato XMLA o TSML (JSON).|<xref:Microsoft.AnalysisServices.Server.Execute%2A>|  
|[Invoke-ProcessASDatabase](../../analysis-services/powershell/invoke-processasdatabase.md)|Procesar una base de datos.|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Cmdlet Invoke-ProcessCube](../../analysis-services/powershell/invoke-processcube-cmdlet.md)|Procesar un cubo.|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Cmdlet Invoke-ProcessDimension](../../analysis-services/powershell/invoke-processdimension-cmdlet.md)|Procesar una dimensión.|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Cmdlet Invoke-ProcessPartition](../../analysis-services/powershell/invoke-processpartition-cmdlet.md)|Procesar una partición.|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Cmdlet Invoke-ProcessTable](../../analysis-services/powershell/invoke-processtable-cmdlet.md)|Procesar una tabla en un modelo tabular, un modelo de compatibilidad 1200 o posterior.|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Cmdlet Merge-Partition](../../analysis-services/powershell/merge-partition-cmdlet.md)|Combinar una partición.|<xref:Microsoft.AnalysisServices.Partition.Merge%2A>|  
|[Cmdlet New-RestoreFolder](../../analysis-services/powershell/new-restorefolder-cmdlet.md)|Crear una carpeta que contenga una copia de seguridad de la base de datos.|<xref:Microsoft.AnalysisServices.RestoreFolder>|  
|[Cmdlet New-RestoreLocation](../../analysis-services/powershell/new-restorelocation-cmdlet.md)|Especificar uno o varios servidores remotos en los que restaurar la base de datos.|<xref:Microsoft.AnalysisServices.RestoreLocation>|  
|[Cmdlet Remove-RoleMember](../../analysis-services/powershell/remove-rolemember-cmdlet.md)|Quitar un miembro de un rol de base de datos.|<xref:Microsoft.AnalysisServices.RoleMemberCollection.Remove%2A>|  
|[Cmdlet Restore-ASDatabase](../../analysis-services/powershell/restore-asdatabase-cmdlet.md)|Restaurar una base de datos en una instancia de servidor.|<xref:Microsoft.AnalysisServices.Server.Restore%2A>|  
  
## Vea también  
 [Tabular Model Scripting Language &#40;TMSL&#41; Reference (Referencia de Tabular Model Scripting Language [TMSL])](../Topic/Tabular%20Model%20Scripting%20Language%20\(TMSL\)%20Reference.md)   
 [Nivel de compatibilidad para modelos tabulares de Analysis Services](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)   
 [Referencia de Analysis Services Scripting Language &#40;ASSL&#41;](../../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md)   
 [PowerShell scripting in Analysis Services](../../analysis-services/instances/powershell-scripting-in-analysis-services.md)  
  
  