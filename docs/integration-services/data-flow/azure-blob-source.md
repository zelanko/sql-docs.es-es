---
title: Origen de blob de Azure | Microsoft Docs
ms.custom: ''
ms.date: 08/20/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.afpblobsrc.f1
- sql14.dts.designer.afpblobsrc.f1
ms.assetid: 80645c5c-88c8-4fb0-8607-de1bb7bffcbb
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5404b7bc7e7543f85890816973fdbd0c1e39022f
ms.sourcegitcommit: 61212c06b56953ce2e2627d35f7bd69cda786540
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2018
ms.locfileid: "40405865"
---
# <a name="azure-blob-source"></a>Origen de blobs de Azure
  El componente **Azure Blob Source** (Origen de blobs de Azure) permite que un paquete SSIS lea datos de un blob de Azure. Los formatos de archivo admitidos son: CSV y AVRO.
  
  Para ver el editor del origen de blob de Azure, arrastre y coloque el **origen de blob de Azure** en el diseñador de flujos de datos y haga doble clic en él para abrir el editor.  
  
 **Origen de blob de Azure** es un componente de [Feature Pack de SQL Server Integration Services (SSIS) para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).  
  
1.  En el campo **Azure storage connection manager** (Administrador de conexiones de almacenamiento de Azure), especifique un administrador de conexiones de almacenamiento de Azure existente o cree uno nuevo que haga referencia a una cuenta de almacenamiento de Azure.  
  
2.  En el campo **Nombre de contenedor de blobs** , especifique el nombre del contenedor de blobs que contiene los archivos de origen.  
  
3.  En el campo **Nombre de blob** , especifique la ruta de acceso al blob.  
  
4.  En el campo **Blob file format** (Formato de archivo de blob), especifique el formato de blob que desea utilizar: **Text** o **Avro**.  
  
5.  Si el formato de archivo es **Text**, debe especificar el valor **Carácter de delimitador de columna**. (No se admiten los delimitadores con varios caracteres).

    Seleccione también **Nombres de columna de la primera fila de datos** si la primera fila del archivo contiene nombres de columna.

6.  Si el archivo está comprimido, seleccione **Decompress the file** (Descomprimir el archivo).

7.  Si el archivo está comprimido, seleccione el **Tipo de compresión**: **GZIP**, **DEFLATE** o **BZIP2**. Tenga en cuenta que no se admite el formato Zip.
  
8.  Después de especificar la información de conexión, cambie a la página **Columnas** para asignar columnas de origen a columnas de destino para el flujo de datos SSIS.  
  
  
