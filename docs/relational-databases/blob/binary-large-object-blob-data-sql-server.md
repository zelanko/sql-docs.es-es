---
title: Datos de objeto binario grande (Blob) (SQL Server) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-blob
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- FILESTREAM [SQL Server], design and implementation
ms.assetid: 97509274-c3f8-43e5-a37c-52f1ffe0961a
caps.latest.revision: 39
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 4a9291aa99091d1b44e4b829af803637250bd333
ms.lasthandoff: 04/11/2017

---
# <a name="binary-large-object-blob-data-sql-server"></a>Datos de objeto binario grande (Blob) (SQL Server)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona soluciones para almacenar archivos y documentos en la base de datos o en dispositivos de almacenamiento remoto.  
  
##  <a name="section"></a> En esta sección  
 [Comparar opciones para almacenar blobs &#40;SQL Server&#41;](../../relational-databases/blob/compare-options-for-storing-blobs-sql-server.md)  
 Comparar las ventanas de FILESTREAM, FileTables y almacén remoto de blobs.  
  
 [FILESTREAM &#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md)  
 FILESTREAM permite a las aplicaciones basadas en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]almacenar datos no estructurados, como documentos e imágenes, en el sistema de archivos. Las aplicaciones pueden aprovechar las API de transmisión de datos enriquecidas y el rendimiento del sistema de archivos al mismo tiempo que mantienen la coherencia transaccional entre los datos no estructurados y los datos estructurados correspondientes.  
  
 [FileTables &#40;SQL Server&#41;](../../relational-databases/blob/filetables-sql-server.md)  
 La característica FileTable proporciona compatibilidad con el espacio de nombres de archivo de Windows y con las aplicaciones Windows para los datos de archivo almacenados en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. FileTable permite que una aplicación pueda integrar sus componentes de administración de datos y almacenamiento, así como proporcionar servicios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] integrados (incluidas la búsqueda de texto completo y la búsqueda semántica) en datos y metadatos no estructurados.  
  
 Es decir, ahora puede almacenar archivos y documentos en tablas especiales de FileTables denominadas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y tener acceso a ellos desde las aplicaciones Windows como si estuviesen almacenados en el sistema de archivos, sin efectuar cambios en las aplicaciones cliente.  
  
 [Almacén remoto de blobs &#40;RBS&#41; &#40;SQL Server&#41;](../../relational-databases/blob/remote-blob-store-rbs-sql-server.md)  
 El almacén remoto de blobs (RBS) para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite a los administradores de bases de datos almacenar directamente objetos binarios grandes (blobs) en soluciones de almacenamiento estándar en lugar de directamente en el servidor. De este modo se ahorra una cantidad de espacio significativa y se evita malgastar los caros recursos de hardware de los servidores. RBS proporciona un conjunto de bibliotecas API que definen un modelo normalizado para que las aplicaciones accedan a los datos de los BLOB. RBS también incluye herramientas de mantenimiento, como la recolección de elementos no utilizados, para ayudar a administrar los datos BLOB remotos.  
  
 RBS se incluye en el disco de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y pero no lo instala el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
  
