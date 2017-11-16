---
title: Algoritmos de complemento | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- third-party algorithms [Analysis Services]
- algorithms [data mining], creating
- plugin algorithms [Analysis Services]
ms.assetid: fe364ddc-576e-42fc-9ced-baa399992f92
caps.latest.revision: 25
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 66fad2d8974e832925ab67174f2c635b8f5fbf37
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="plugin-algorithms"></a>Algoritmos de complemento
  Además de los algoritmos que proporciona [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] existen muchos otros algoritmos que puede usar en la minería de datos. Así, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ofrece un mecanismo para que los algoritmos creados por otros fabricantes puedan ser un "complemento". Siempre que el algoritmo cumpla ciertos estándares, podrá utilizarlos en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de forma similar a los algoritmos de [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Los algoritmos de complemento tienen todas las capacidades de los algoritmos que proporciona [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 Para obtener una descripción completa de las interfaces que [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] utiliza para comunicarse con algoritmos de complemento, vea los ejemplos para crear un algoritmo y un visor de modelos personalizados que se publiquen en el sitio sitio Web de [CodePlex](http://go.microsoft.com/fwlink/?LinkID=87843) .  
  
## <a name="algorithm-requirements"></a>Requisitos de los algoritmos  
 Para usar un algoritmo de complemento en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], debe implementar las siguientes interfaces COM:  
  
 **IDMAlgorithm**  
 Implementa un algoritmo que genera modelos e implementa las operaciones de predicción de los modelos resultantes.  
  
 **IDMAlgorithmNavigation**  
 Habilita el acceso de los exploradores al contenido de los modelos.  
  
 **IDMPersist**  
 Permite que [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]guarde y cargue los modelos que entrena el algoritmo.  
  
 **IDMAlgorithmMetadata**  
 Describe las capacidades y los parámetros de entrada del algoritmo.  
  
 **IDMAlgorithmFactory**  
 Crea instancias de los objetos que implementan la interfaz del algoritmo y permite que [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tenga acceso a la interfaz de metadatos del algoritmo.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] utiliza las interfaces COM para comunicarse con los algoritmos de complemento. Aunque los algoritmos de complemento que utilice deben admitir la especificación [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB para minería de datos, no tienen que admitir todas las opciones de minería de datos de la especificación. Puede usar el conjunto de filas de esquema [MINING_SERVICES](../../analysis-services/schema-rowsets/data-mining/dmschema-mining-services-rowset.md) para determinar las capacidades del algoritmo. Este conjunto de filas de esquema presenta una lista de las opciones de compatibilidad de la minería de datos con cada proveedor de algoritmos de complemento.  
  
 Debe registrar los nuevos algoritmos antes de usarlos en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Para registrar un algoritmo, incluya la siguiente información en el archivo .ini de la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en la que desea incluir los algoritmos:  
  
-   El nombre del algoritmo  
  
-   ProgID (esto es opcional y solo se incluirá con los algoritmos de complemento)  
  
-   Una marca que determine si el algoritmo está o no habilitado  
  
 El siguiente ejemplo de código muestra cómo registrar un algoritmo nuevo:  
  
 `<ConfigurationSettings>`  
  
 `...`  
  
 `<DataMining>`  
  
 `...`  
  
 `<Algorithms>`  
  
 `...`  
  
 `<Sample_Plugin_Algorithm>`  
  
 `<Enabled>1</Enabled>`  
  
 `<ProgID>Microsoft.DataMining.SamplePlugInAlgorithm.Factory</ProgID>`  
  
 `</Sample_PlugIn_Algorithm>`  
  
 `...`  
  
 `</Algorithms>`  
  
 `...`  
  
 `</DataMining>`  
  
 `...`  
  
 `</ConfigurationSettings>`  
  
## <a name="see-also"></a>Vea también  
 [Algoritmos de minería de datos &#40;Analysis Services: Minería de datos&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Conjunto de filas DMSCHEMA_MINING_SERVICES](../../analysis-services/schema-rowsets/data-mining/dmschema-mining-services-rowset.md)  
  
  

