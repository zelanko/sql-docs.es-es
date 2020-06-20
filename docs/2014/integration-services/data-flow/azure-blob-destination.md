---
title: Destino de blob de Azure | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.afpblobdest.f1
- sql11.dts.designer.afpblobdest.f1
ms.assetid: 820a1e7a-7182-4c7b-ab56-5b4097a7e042
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 5a64cfd2385cb510163ca5c2f66db64a86dd00bc
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84916695"
---
# <a name="azure-blob-destination"></a>Destino de blobs de Azure
  El componente **Azure Blob Destination** (Destino de blobs de Azure) permite que un paquete SSIS escriba datos en un blob de Azure. Los formatos de archivo admitidos son: CSV y AVRO. Arrastre: Quite el **destino de BLOB de Azure** al diseñador de flujo de datos y haga doble clic en él para ver el editor).  
  
1.  En el campo **Azure storage connection manager** (Administrador de conexiones de Azure Storage), especifique un administrador de conexiones de Azure Storage existente o cree uno nuevo que haga referencia a una cuenta de Azure Storage.  
  
2.  En el campo **Nombre de contenedor de blobs** , especifique el nombre del contenedor de blobs que contiene los archivos de origen.  
  
3.  En el campo **Nombre de blob** , especifique la ruta de acceso al blob.  
  
4.  En el campo **Blob file format** (Formato de archivo de blob), especifique el formato de blob que desea utilizar.  
  
5.  Si el formato de archivo es CSV, debe especificar el valor **Column delimiter character** (Carácter delimitador de columna). Seleccione también **nombres de columna en la primera fila de datos** si la primera fila del archivo contiene nombres de columna.  
  
6.  Después de especificar la información de conexión, cambie a la página **Columnas** para asignar columnas de origen a columnas de destino para el flujo de datos SSIS.  
  
  
