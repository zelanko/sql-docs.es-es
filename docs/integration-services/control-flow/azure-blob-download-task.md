---
title: Tarea de descarga de blobs de Azure | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.afpblobdltask.f1
- sql14.dts.designer.afpblobdltask.f1
ms.assetid: 8a63bf44-71be-456d-9a5c-be7c31aff065
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: ec05684572563228ec3bce88ebb5c5ca32a86bc2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66403207"
---
# <a name="azure-blob-download-task"></a>Tarea de descarga de blobs de Azure

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


La tarea de descarga de blobs de Azure permite a un paquete SSIS descargar archivos desde un almacenamiento de blobs de Azure.

Para agregar una **tarea de descarga de blobs de Azure**, arrástrela y suéltela en el Diseñador SSIS y haga doble clic (o haga clic con el botón derecho y, después, haga clic en **Editar** ) para ver el siguiente cuadro de diálogo del **Editor de la tarea de descarga de blobs de Azure** .  
  
 La **tarea de descarga de blobs de Azure** es un componente de [Feature Pack de SQL Server Integration Services (SSIS) para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).  
  
 En la tabla siguiente se proporciona la descripción de los campos de este cuadro de diálogo.  

|**Campo**|**Descripción**|  
|---|---|
|AzureStorageConnection|Especifique un administrador de conexiones de almacenamiento de Azure existente o cree uno nuevo que haga referencia a una cuenta de almacenamiento de Azure, que esté orientado a la ubicación en la que se encuentran hospedados los archivos de blob.|  
|BlobContainer|Especifica el nombre del contenedor de blobs que contiene los archivos de blob que hay que descargar.|  
|BlobDirectory|Especifica el directorio de blobs que contiene los archivos de blob que hay que descargar. El directorio de blob es una estructura jerárquica virtual.|  
|SearchRecursively|Especifica si se debe buscar de forma recursiva en subdirectorios.|  
|LocalDirectory|Especifica el directorio local en el que se almacenan los archivos de blob descargados.|  
|FileName|Especifica un filtro de nombre para seleccionar archivos con el patrón de nombre especificado. Por ejemplo, `MySheet*.xls\*` incluye archivos como `MySheet001.xls` y `MySheetABC.xlsx`.|  
|TimeRangeFrom/TimeRangeTo|Especifica un filtro de intervalo de tiempo. Se incluyen los archivos modificados después de **TimeRangeFrom** y antes de **TimeRangeTo**.|  
