---
title: Tarea de carga de blobs de Azure | Documentos de Microsoft
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
- sql13.dts.designer.afpblobuptask.f1
- sql14.dts.designer.afpblobuptask.f1
ms.assetid: 6ea068b0-4cd8-45b5-b89d-09b8f25040c0
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: cec51398ac521abc0345e90b3c6ed156b542b5f1
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="azure-blob-upload-task"></a>Tarea de carga de blobs de Azure
La **tarea de carga de blobs de Azure** permite a un paquete SSIS cargar archivos a un almacenamiento de blobs de Azure.
    
Para agregar una **tarea de carga de blobs de Azure**, arrástrela y colóquela en el Diseñador SSIS, haga doble clic o haga clic con el botón derecho y, luego, haga clic en **Editar** para ver el siguiente cuadro de diálogo del **Azure Blob Upload Task Editor** (Editor de la tarea de carga de blobs de Azure).  
  
 El **tarea de carga de blobs de Azure** es un componente de la [SQL Server Integration Services (SSIS) Feature Pack para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).
  
 En la tabla siguiente se proporcionan las descripciones de los campos de este cuadro de diálogo.  
  
|||  
|-|-|  
|**Campo**|**Description**|  
|AzureStorageConnection|Especifique un administrador de conexiones de almacenamiento de Azure existente o cree uno nuevo que haga referencia a una cuenta de almacenamiento de Azure, que esté orientado a la ubicación en la que se encuentran hospedados los archivos de blob.|  
|BlobContainer|Especifica el nombre del contenedor de blob que contiene los archivos cargados como blobs.|  
|BlobDirectory|Especifica el directorio de blob donde se almacena el archivo cargado como un blob en bloques. El directorio de blob es una estructura jerárquica virtual. Si el blob ya existe, se reemplaza.|  
|LocalDirectory|Especifica el directorio local que contiene los archivos que se van a cargar.|  
|FileName|Especifica un filtro de nombre para seleccionar archivos con el patrón de nombre especificado. Por ejemplo, `MySheet*.xls\*` incluye archivos como `MySheet001.xls` y `MySheetABC.xlsx`.|  
|TimeRangeFrom/TimeRangeTo|Especifica un filtro de intervalo de tiempo. Archivos modificados después **TimeRangeFrom** y antes de **TimeRangeTo** se incluyen.|  
  
  

