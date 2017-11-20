---
title: Destino de blobs de Azure | Documentos de Microsoft
ms.custom: 
ms.date: 07/25/2016
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.afpblobdest.f1
- sql14.dts.designer.afpblobdest.f1
ms.assetid: 820a1e7a-7182-4c7b-ab56-5b4097a7e042
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 152d92859c2f4ce96d0cc1ba9b02ffb412d18fde
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="azure-blob-destination"></a>Destino de blobs de Azure
 El componente **Azure Blob Destination** (Destino de blobs de Azure) permite que un paquete SSIS escriba datos en un blob de Azure. Los formatos de archivo admitidos son: CSV y AVRO. 
   
 Arrastre y coloque el **destino de blobs de Azure** en el diseñador de flujos de datos y haga doble clic en él para ver el editor.  
  
 El **destino de Blob de Azure** es un componente de la [SQL Server Integration Services (SSIS) Feature Pack para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).  
  
1.  En el campo **Azure storage connection manager** (Administrador de conexiones de almacenamiento de Azure), especifique un administrador de conexiones de almacenamiento de Azure existente o cree uno nuevo que haga referencia a una cuenta de almacenamiento de Azure.  
  
2.  En el campo **Nombre de contenedor de blobs** , especifique el nombre del contenedor de blobs que contiene los archivos de origen.  
  
3.  En el campo **Nombre de blob** , especifique la ruta de acceso al blob.  
  
4.  En el campo **Blob file format** (Formato de archivo de blob), especifique el formato de blob que desea utilizar.  
  
5.  Si el formato de archivo es CSV, debe especificar el valor **Column delimiter character** (Carácter delimitador de columna). Seleccione también **Nombres de columna de la primera fila de datos** si la primera fila del archivo contiene nombres de columna.  
  
6.  Después de especificar la información de conexión, cambie a la página **Columnas** para asignar columnas de origen a columnas de destino para el flujo de datos SSIS.  
  
  

