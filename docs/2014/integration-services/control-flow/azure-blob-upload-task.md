---
title: Tarea de carga de blobs de Azure | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.afpblobuptask.f1
- sql11.dts.designer.afpblobuptask.f1
ms.assetid: 6ea068b0-4cd8-45b5-b89d-09b8f25040c0
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d0f0e4123a16eb82000c6506dc7bcb62b353a268
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37188562"
---
# <a name="azure-blob-upload-task"></a>Tarea de carga de blobs de Azure
  La tarea de carga de blobs de Azure permite que un paquete SSIS cargar archivos en Azure blob storage.   
Para agregar una **tarea de carga de blobs de Azure**, arrástrela y colóquela en el Diseñador SSIS, haga doble clic o haga clic con el botón derecho y, luego, haga clic en **Editar** para ver el siguiente cuadro de diálogo del **Azure Blob Upload Task Editor** (Editor de la tarea de carga de blobs de Azure).  
  
 En la tabla siguiente se proporcionan las descripciones de los campos de este cuadro de diálogo.  
  
|||  
|-|-|  
|**Campo**|**Descripción**|  
|AzureStorageConnection|Especifique un administrador de conexiones de almacenamiento de Azure existente o cree uno nuevo que haga referencia a una cuenta de almacenamiento de Azure, que esté orientado a la ubicación en la que se encuentran hospedados los archivos de blob.|  
|BlobContainer|Especifica el nombre del contenedor de blobs que contendrá los archivos cargados como blobs.|  
|BlobDirectory|Especifica el directorio de blobs donde se almacenará el archivo cargado como un blob en bloques. El directorio de blob es una estructura jerárquica virtual. Si ya existe el blob, se reemplazará.|  
|LocalDirectory|Especifica el directorio local que contiene los archivos que se van a cargar.|  
|FileName|Especifica un filtro de nombre para seleccionar archivos con el patrón de nombre especificado. Por ejemplo: MiHoja*.xls\* incluirá archivos como MiHoja001.xls y MiHojaABC.xlsx.|  
|TimeRangeFrom/TimeRangeTo|Especifica un filtro de intervalo de tiempo. Se incluirán los archivos modificados después de **TimeRangeFrom** y antes de **TimeRangeTo** .|  
  
  
