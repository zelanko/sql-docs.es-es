---
title: Programar objetos de minería de datos AMO | Documentos de Microsoft
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- programming [AMO]
- data mining [AMO]
- AMO, data mining
- Analysis Management Objects, data mining
ms.assetid: d27f58b9-91be-449c-8403-439aa6dd1ff9
caps.latest.revision: 19
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 62ef444d7fa112267a4a272553834e24fe5b0df9
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36198556"
---
# <a name="programming-amo-data-mining-objects"></a>Programar objetos de minería de datos con AMO
  La programación de objetos de minería de datos mediante AMO es un proceso sencillo y directo. El primer paso consiste en crear un modelo de estructura de datos que admita el proyecto de minería de datos. A continuación, se crea el modelo de minería de datos que admite el algoritmo de minería de datos que desea utilizar para predecir o buscar las relaciones ocultas subyacentes a los datos. Una vez creado el proyecto de minería de datos (incluidos la estructura y los algoritmos), puede procesar los modelos de minería de datos para obtener los modelos entrenados que utilizará más adelante al realizar consultas y predicciones desde la aplicación cliente.  
  
 Es necesario recordar que AMO no se utiliza para realizar consultas, sino para administrar las estructuras y los modelos de minería de datos. Para consultar los datos, use [desarrollar con ADOMD.NET](../adomd-net/developing-with-adomd-net.md).  
  
 Este tema contiene las siguientes secciones:  
  
-   [Objetos MiningStructure](#MiningStructure)  
  
-   [Objetos MiningModel](#MiningModel)  
  
##  <a name="MiningStructure"></a> Objetos MiningStructure  
 Una estructura de minería de datos es la definición de la estructura de datos que se utiliza para crear todos los modelos de minería de datos. Una estructura de minería de datos contiene un enlace a una vista del origen de datos definida en la base de datos y contiene definiciones de todas las columnas que participan en los modelos de minería de datos. Una estructura de minería de datos puede tener más de un modelo.  
  
 La creación de un objeto <xref:Microsoft.AnalysisServices.MiningStructure> requiere los pasos siguientes:  
  
1.  Crear el objeto <xref:Microsoft.AnalysisServices.MiningStructure> y rellenar los atributos básicos. Entre los atributos básicos se incluyen el nombre del objeto, el id. de objeto (identificación interna) y el enlace del origen de datos.  
  
2.  Crear columnas para el modelo. Las columnas pueden ser de tipo escalar o definiciones de tabla.  
  
     Cada columna requiere un nombre y un id. interno, un tipo, una definición del contenido y un enlace.  
  
3.  Actualizar el objeto <xref:Microsoft.AnalysisServices.MiningStructure> en el servidor mediante el método Update del objeto.  
  
     Las estructuras de minería de datos se pueden procesar y, al procesarlas, se procesan o se vuelven a entrenar los modelos de minería de datos secundarios.  
  
 El código de ejemplo siguiente crea una estructura de minería de datos para pronosticar las ventas en una serie temporal. Antes de ejecutar el ejemplo de código, asegúrese de que la base de datos *db*, pasado como parámetro para `CreateSalesForecastingMiningStructure`, contiene en `db.DataSourceViews[0]` una referencia a la vista *dbo.vTimeSeries* en el [!INCLUDE[ssAWDWsp](../../../includes/ssawdwsp-md.md)]base de datos de ejemplo.  
  
```  
public static MiningStructure CreateSalesForecastingMiningStructure(Database db)  
{  
    MiningStructure ms = db.MiningStructures.FindByName("Forecasting Sales Structure");  
    if (ms != null)  
        ms.Drop();  
    ms = db.MiningStructures.Add("Forecasting Sales Structure", "Forecasting Sales Structure");  
    ms.Source = new DataSourceViewBinding(db.DataSourceViews[0].ID);  
  
    ScalarMiningStructureColumn amount = ms.Columns.Add("Amount", "Amount");  
    amount.Type = MiningStructureColumnTypes.Double;  
    amount.Content = MiningStructureColumnContents.Continuous;  
    amount.KeyColumns.Add("vTimeSeries", "Amount", OleDbType.Currency);  
  
    ScalarMiningStructureColumn modelRegion = ms.Columns.Add("Model Region", "Model Region");  
    modelRegion.IsKey = true;  
    modelRegion.Type = MiningStructureColumnTypes.Text;  
    modelRegion.Content = MiningStructureColumnContents.Key;  
    modelRegion.KeyColumns.Add("vTimeSeries", "ModelRegion", OleDbType.WChar, 56);  
  
    ScalarMiningStructureColumn qty = ms.Columns.Add("Quantity", "Quantity");  
    qty.Type = MiningStructureColumnTypes.Long;  
    qty.Content = MiningStructureColumnContents.Continuous;  
    qty.KeyColumns.Add("vTimeSeries", "Quantity", OleDbType.Integer);  
  
    ScalarMiningStructureColumn timeIndex = ms.Columns.Add("TimeIndex", "TimeIndex");  
    timeIndex.IsKey = true;  
    timeIndex.Type = MiningStructureColumnTypes.Long;  
    timeIndex.Content = MiningStructureColumnContents.KeyTime;  
    timeIndex.KeyColumns.Add("vTimeSeries", "TimeIndex", OleDbType.Integer);  
  
    ms.Update();  
    return ms;  
}  
```  
  
##  <a name="MiningModel"></a> Objetos MiningModel  
 Un modelo de minería de datos es un repositorio de todas las columnas y definiciones de columna que se utilizarán en un algoritmo de minería de datos.  
  
 La creación de un objeto <xref:Microsoft.AnalysisServices.MiningModel> requiere los pasos siguientes:  
  
1.  Crear el objeto <xref:Microsoft.AnalysisServices.MiningModel> y rellenar los atributos básicos.  
  
     Entre los atributos básicos se incluyen el nombre del objeto, el id. de objeto (identificación interna) y la especificación del algoritmo de minería de datos.  
  
2.  Agregar las columnas del modelo de minería de datos. Una de las columnas debe definirse como clave de caso.  
  
3.  Actualizar el objeto <xref:Microsoft.AnalysisServices.MiningModel> en el servidor mediante el método Update del objeto.  
  
     Los objetos <xref:Microsoft.AnalysisServices.MiningModel> se pueden procesar con independencia de otros modelos en el elemento <xref:Microsoft.AnalysisServices.MiningStructure> primario.  
  
 El código de ejemplo siguiente crea un modelo de pronóstico de serie temporal de Microsoft basado en la estructura de minería de datos "Forecasting Sales Structure":  
  
```  
public static MiningModel CreateSalesForecastingMiningModel(MiningStructure ms)  
{  
    if (ms.MiningModels.ContainsName("Sales Forecasting Model"))  
    {  
        ms.MiningModels["Sales Forecasting Model"].Drop();  
    }  
    MiningModel mm = ms.CreateMiningModel(true, "Sales Forecasting Model");  
    mm.Algorithm = MiningModelAlgorithms.MicrosoftTimeSeries;  
    mm.AlgorithmParameters.Add("PERIODICITY_HINT", "{12}");  
  
    MiningModelColumn amount = new MiningModelColumn();  
    amount.SourceColumnID = "Amount";  
    amount.Usage = MiningModelColumnUsages.Predict;  
  
    MiningModelColumn modelRegion = new MiningModelColumn();  
    modelRegion.SourceColumnID = "Model Region";  
    modelRegion.Usage = MiningModelColumnUsages.Key;  
  
    MiningModelColumn qty = new MiningModelColumn();  
    qty.SourceColumnID = "Quantity";  
    qty.Usage = MiningModelColumnUsages.Predict;  
  
    MiningModelColumn ti = new MiningModelColumn();  
    ti.SourceColumnID = "TimeIndex";  
    ti.Usage = MiningModelColumnUsages.Key;  
  
    mm.Update();  
    mm.Process(ProcessType.ProcessFull);  
    return mm;  
}  
```  
  
## <a name="see-also"></a>Vea también  
 <xref:Microsoft.AnalysisServices>   
 [Clases fundamentales de AMO](amo-fundamental-classes.md)   
 [Introducción a las clases AMO](amo-classes-introduction.md)   
 [Clases de minería de datos AMO](amo-data-mining-classes.md)   
 [Arquitectura lógica &#40;Analysis Services - datos multidimensionales&#41;](../olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [Objetos de base de datos &#40;Analysis Services - datos multidimensionales&#41;](../olap-logical/database-objects-analysis-services-multidimensional-data.md)  
  
  