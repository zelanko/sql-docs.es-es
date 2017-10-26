---
title: Tarea de descarga de blobs de Azure | Documentos de Microsoft
ms.custom:
- SQL2016_New_Updated
ms.date: 07/25/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.afpblobdltask.f1
- sql14.dts.designer.afpblobdltask.f1
ms.assetid: 8a63bf44-71be-456d-9a5c-be7c31aff065
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 95ea7de4600551cc994e82dd3408cb4ea608685c
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="azure-blob-download-task"></a>Tarea de descarga de blobs de Azure
La tarea de descarga de blobs de Azure permite a un paquete SSIS descargar archivos desde un almacenamiento de blobs de Azure.

Para agregar una **tarea de descarga de blobs de Azure**, arrástrela y suéltela en el Diseñador SSIS y haga doble clic o haga clic con el botón secundario y luego haga clic en **Editar** para ver el siguiente cuadro de diálogo de **Editor de la tarea de descarga de blobs de Azure** .  
  
 El **tarea de descarga de blobs de Azure** es un componente de la [SQL Server Integration Services (SSIS) Feature Pack para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).  
  
 En la tabla siguiente se proporciona la descripción de los campos de este cuadro de diálogo.  
  
|||  
|-|-|  
|**Campo**|**Description**|  
|AzureStorageConnection|Especifique un administrador de conexiones de almacenamiento de Azure existente o cree uno nuevo que haga referencia a una cuenta de almacenamiento de Azure, que esté orientado a la ubicación en la que se encuentran hospedados los archivos de blob.|  
|BlobContainer|Especifica el nombre del contenedor de blobs que contiene los archivos de blob que hay que descargar.|  
|BlobDirectory|Especifica el directorio de blobs que contiene los archivos de blob que hay que descargar. El directorio de blob es una estructura jerárquica virtual.|  
|LocalDirectory|Especifica el directorio local donde se almacenan los archivos de blob descargados.|  
|FileName|Especifica un filtro de nombre para seleccionar archivos con el patrón de nombre especificado. Por ejemplo, `MySheet*.xls\*` incluye archivos como `MySheet001.xls` y `MySheetABC.xlsx`.|  
|TimeRangeFrom/TimeRangeTo|Especifica un filtro de intervalo de tiempo. Archivos modificados después **TimeRangeFrom** y antes de **TimeRangeTo** se incluyen.|  
  
  

