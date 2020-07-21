---
title: Representación de partición (tabular) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
ms.assetid: b606cd63-755c-4ac0-b19b-95b5363afbdf
author: minewiskan
ms.author: owend
ms.openlocfilehash: 6a29f273a584f3e60c6cf6458751965158cf8704
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84940006"
---
# <a name="partition-representation-tabular"></a>Representación de partición (tabular)
  A efectos operativos, una tabla se puede dividir en distintos subconjuntos de filas que, al combinarse, forman la tabla. Cada uno de los subconjuntos es una partición de la tabla.  
  
## <a name="partition-representation"></a>Representación de partición  
 Por lo que respecta a los objetos de AMO, las representaciones de particiones tienen una relación de asignación uno a uno con <xref:Microsoft.AnalysisServices.Partition> y no se necesitan otros objetos principales de AMO.  
  
### <a name="partition-in-amo"></a>Partición en AMO  
 Cuando se usa AMO para administrar una partición, es necesario buscar el grupo de medida que representa la tabla modelo tabular y trabajar desde allí.  
  
 En el fragmento de código siguiente se muestra cómo se agrega una partición a una tabla modelo existente.  
  
```  
  
private void AddPartition(  
                     AMO.Cube modelCube  
                  ,  AMO.DataSource newDatasource  
                  ,  string mgName  
                  ,  string newPartitionName  
                  , string partitionSelectStatement  
                  , Boolean processPartition  
             )  
{  
    mgName = mgName.Trim();  
    newPartitionName = newPartitionName.Trim();  
    partitionSelectStatement = partitionSelectStatement.Trim();  
    //Validate Input  
    if (string.IsNullOrEmpty(newPartitionName) || string.IsNullOrWhiteSpace(newPartitionName))  
    {  
        MessageBox.Show(String.Format("Partition Name cannot be empty or blank"), "AMO to Tabular message", MessageBoxButtons.OK, MessageBoxIcon.Error);  
        return;  
    }  
  
    if (modelCube.MeasureGroups[mgName].Partitions.ContainsName(newPartitionName))  
    {  
        MessageBox.Show(String.Format("Partition Name already defined. Duplicated names are not allowed"), "AMO to Tabular message", MessageBoxButtons.OK, MessageBoxIcon.Error);  
        return;  
    }  
  
    if (string.IsNullOrEmpty(partitionSelectStatement) || string.IsNullOrWhiteSpace(partitionSelectStatement))  
    {  
        MessageBox.Show(String.Format("Select statement cannot be empty or blank"), "AMO to Tabular message", MessageBoxButtons.OK, MessageBoxIcon.Error);  
        return;  
    }  
  
    //Input validated  
    string partitionID = newPartitionName; //Using partition name as the ID  
    AMO.Partition currentPartition = new AMO.Partition(partitionID, partitionID);  
    currentPartition.StorageMode = AMO.StorageMode.InMemory;  
    currentPartition.ProcessingMode = AMO.ProcessingMode.Regular;  
    currentPartition.Source = new AMO.QueryBinding(newDatasource.ID, partitionSelectStatement);  
    modelCube.MeasureGroups[mgName].Partitions.Add(currentPartition);  
    try  
    {  
        modelCube.Update(AMO.UpdateOptions.ExpandFull, AMO.UpdateMode.UpdateOrCreate);  
        if (processPartition)  
        {  
            modelCube.MeasureGroups[mgName].Partitions[partitionID].Process(AMO.ProcessType.ProcessFull);  
            MessageBox.Show(String.Format("Partition successfully processed."), "AMO to Tabular message", MessageBoxButtons.OK, MessageBoxIcon.Information);  
        }  
  
    }  
    catch (AMO.AmoException amoXp)  
    {  
        MessageBox.Show(String.Format("AMO exception accessing the server.\nError message: {0}", amoXp.Message), "AMO to Tabular message", MessageBoxButtons.OK, MessageBoxIcon.Warning);  
        return;  
    }  
    catch (Exception)  
    {  
        throw;  
    }  
}  
  
```  
  
## <a name="amo2tabular-sample"></a>Ejemplo AMO2Tabular  
 Sin embargo, para saber cómo usar AMO para crear y manipular representaciones de partición vea el código fuente del ejemplo AMO a tabular. El ejemplo está disponible en Codeplex. Nota importante sobre el código: el código se proporciona solo como apoyo de los conceptos lógicos explicados aquí y no debe utilizarse en un entorno de producción; no debe usarse para otros fines excepto el pedagógico.  
  
  
