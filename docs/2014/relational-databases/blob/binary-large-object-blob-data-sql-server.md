---
title: Datos de objeto binario grande (Blob) (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], design and implementation
ms.assetid: 97509274-c3f8-43e5-a37c-52f1ffe0961a
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 7f549f1c851ff09b165dae055b8bb18f01a66fcb
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/22/2019
ms.locfileid: "66010339"
---
# <a name="binary-large-object-blob-data-sql-server"></a>Datos de objeto binario grande (Blob) (SQL Server)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona soluciones para almacenar archivos y documentos en la base de datos o en dispositivos de almacenamiento remoto.  
  
##  <a name="section"></a> En esta sección  
 [Comparar opciones para almacenar blobs &#40;SQL Server&#41;](compare-options-for-storing-blobs-sql-server.md)  
 Comparar las ventanas de FILESTREAM, FileTables y almacén remoto de blobs.  
  
 [FILESTREAM &#40;SQL Server&#41;](filestream-sql-server.md)  
 FILESTREAM permite a las aplicaciones basadas en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]almacenar datos no estructurados, como documentos e imágenes, en el sistema de archivos. Las aplicaciones pueden aprovechar las API de transmisión de datos enriquecidas y el rendimiento del sistema de archivos al mismo tiempo que mantienen la coherencia transaccional entre los datos no estructurados y los datos estructurados correspondientes.  
  
 [FileTables &#40;SQL Server&#41;](filetables-sql-server.md)  
 La característica FileTable proporciona compatibilidad con el espacio de nombres de archivo de Windows y con las aplicaciones Windows para los datos de archivo almacenados en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. FileTable permite que una aplicación pueda integrar sus componentes de administración de datos y almacenamiento, así como proporcionar servicios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] integrados (incluidas la búsqueda de texto completo y la búsqueda semántica) en datos y metadatos no estructurados.  
  
 Es decir, ahora puede almacenar archivos y documentos en tablas especiales de FileTables denominadas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y tener acceso a ellos desde las aplicaciones Windows como si estuviesen almacenados en el sistema de archivos, sin efectuar cambios en las aplicaciones cliente.  
  
 [Almacén remoto de blobs &#40;RBS&#41; &#40;SQL Server&#41;](remote-blob-store-rbs-sql-server.md)  
 El almacén remoto de blobs (RBS) para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite a los administradores de bases de datos almacenar directamente objetos binarios grandes (blobs) en soluciones de almacenamiento estándar en lugar de directamente en el servidor. De este modo se ahorra una cantidad de espacio significativa y se evita malgastar los caros recursos de hardware de los servidores. RBS proporciona un conjunto de bibliotecas API que definen un modelo normalizado para que las aplicaciones accedan a los datos de los BLOB. RBS también incluye herramientas de mantenimiento, como la recolección de elementos no utilizados, para ayudar a administrar los datos BLOB remotos.  
  
 RBS se incluye en el disco de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y pero no lo instala el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
  
