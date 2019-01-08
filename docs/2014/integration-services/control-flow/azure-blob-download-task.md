---
title: Tarea de descarga de blobs de Azure | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.afpblobdltask.f1
- sql11.dts.designer.afpblobdltask.f1
ms.assetid: 8a63bf44-71be-456d-9a5c-be7c31aff065
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 06d3feab318f1610e5ccd5290acb2e3a839bb6ab
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52756907"
---
# <a name="azure-blob-download-task"></a>Tarea de descarga de blobs de Azure
  La tarea de descarga de blobs de Azure permite a un paquete SSIS descargar archivos desde un almacenamiento de blobs de Azure.   
Para agregar una **tarea de descarga de blobs de Azure**, arrástrela y suéltela en el Diseñador SSIS y haga doble clic o haga clic con el botón secundario y luego haga clic en **Editar** para ver el siguiente cuadro de diálogo de **Editor de la tarea de descarga de blobs de Azure** .  
  
 En la tabla siguiente se proporciona la descripción de los campos de este cuadro de diálogo.  
  
|||  
|-|-|  
|**Campo**|**Descripción**|  
|AzureStorageConnection|Especifique un administrador de conexiones de almacenamiento de Azure existente o cree uno nuevo que haga referencia a una cuenta de almacenamiento de Azure, que esté orientado a la ubicación en la que se encuentran hospedados los archivos de blob.|  
|BlobContainer|Especifica el nombre del contenedor de blobs que contiene los archivos de blob que hay que descargar.|  
|BlobDirectory|Especifica el directorio de blobs que contiene los archivos de blob que hay que descargar. El directorio de blob es una estructura jerárquica virtual.|  
|LocalDirectory|Especifica el directorio local en el que se almacenarán los archivos de blob descargados.|  
|FileName|Especifica un filtro de nombre para seleccionar archivos con el patrón de nombre especificado. Por ejemplo: MiHoja*.xls\* incluirá archivos como MiHoja001.xls y MiHojaABC.xlsx.|  
|TimeRangeFrom/TimeRangeTo|Especifica un filtro de intervalo de tiempo. Se incluirán los archivos modificados después de **TimeRangeFrom** y antes de **TimeRangeTo** .|  
  
  
