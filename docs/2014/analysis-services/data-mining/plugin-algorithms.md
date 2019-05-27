---
title: Los algoritmos de complemento | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- third-party algorithms [Analysis Services]
- algorithms [data mining], creating
- plugin algorithms [Analysis Services]
ms.assetid: fe364ddc-576e-42fc-9ced-baa399992f92
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ac6494a438f8ecd9c1fb48cc7c2a588cfab9bd9a
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66083170"
---
# <a name="plugin-algorithms"></a>Algoritmos de complemento
  Además de los algoritmos que proporciona [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] existen muchos otros algoritmos que puede usar en la minería de datos. Así, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ofrece un mecanismo para que los algoritmos creados por otros fabricantes puedan ser un "complemento". Siempre que el algoritmo cumpla ciertos estándares, podrá utilizarlos en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de forma similar a los algoritmos de [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Los algoritmos de complemento tienen todas las capacidades de los algoritmos que proporciona [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 Para obtener una descripción completa de las interfaces que [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] utiliza para comunicarse con algoritmos de complemento, vea los ejemplos para crear un algoritmo y un visor de modelos personalizados que se publiquen en el sitio sitio Web de [CodePlex](https://go.microsoft.com/fwlink/?LinkID=87843) .  
  
## <a name="algorithm-requirements"></a>Requisitos de los algoritmos  
 Para usar un algoritmo de complemento en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], debe implementar las siguientes interfaces COM:  
  
 `IDMAlgorithm`  
 Implementa un algoritmo que genera modelos e implementa las operaciones de predicción de los modelos resultantes.  
  
 `IDMAlgorithmNavigation`  
 Habilita el acceso de los exploradores al contenido de los modelos.  
  
 `IDMPersist`  
 Permite que [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]guarde y cargue los modelos que entrena el algoritmo.  
  
 `IDMAlgorithmMetadata`  
 Describe las capacidades y los parámetros de entrada del algoritmo.  
  
 `IDMAlgorithmFactory`  
 Crea instancias de los objetos que implementan la interfaz del algoritmo y permite que [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tenga acceso a la interfaz de metadatos del algoritmo.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] utiliza las interfaces COM para comunicarse con los algoritmos de complemento. Aunque los algoritmos de complemento que utilice deben admitir la especificación [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB para minería de datos, no tienen que admitir todas las opciones de minería de datos de la especificación. Puede usar el conjunto de filas de esquema [MINING_SERVICES](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-services-rowset) para determinar las capacidades del algoritmo. Este conjunto de filas de esquema presenta una lista de las opciones de compatibilidad de la minería de datos con cada proveedor de algoritmos de complemento.  
  
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
 [Algoritmos de minería de datos &#40;Analysis Services: Minería de datos&#41;](data-mining-algorithms-analysis-services-data-mining.md)   
 [Conjunto de filas DMSCHEMA_MINING_SERVICES](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-services-rowset)  
  
  
