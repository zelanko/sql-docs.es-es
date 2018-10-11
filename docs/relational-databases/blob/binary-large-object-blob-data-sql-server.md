---
title: Datos de objeto binario grande (Blob) (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], design and implementation
ms.assetid: 97509274-c3f8-43e5-a37c-52f1ffe0961a
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e98651675b4fa159f172dbcf93b38174df2a7a7a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47765743"
---
# <a name="binary-large-object-blob-data-sql-server"></a>Datos de objeto binario grande (Blob) (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona soluciones para almacenar archivos y documentos en la base de datos o en dispositivos de almacenamiento remoto.  
  
## <a name="compare-options-for-storing-blobs-in-sql-server"></a>Comparar opciones para almacenar blobs en SQL Server

Comparar las ventanas de FILESTREAM, FileTables y almacén remoto de blobs. Consulte [Comparar opciones para almacenar blobs &#40;SQL Server&#41;](../../relational-databases/blob/compare-options-for-storing-blobs-sql-server.md).
  
##  <a name="options-for-storing-blobs"></a>Opciones para almacenar blobs  

### <a name="filestream-40sql-server41relational-databasesblobfilestream-sql-servermd"></a>[FILESTREAM &#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md)  

FILESTREAM permite a las aplicaciones basadas en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] almacenar datos no estructurados, como documentos e imágenes, en el sistema de archivos. Las aplicaciones pueden aprovechar las API de transmisión de datos enriquecidas y el rendimiento del sistema de archivos al mismo tiempo que mantienen la coherencia transaccional entre los datos no estructurados y los datos estructurados correspondientes.  
  
### <a name="filetables-40sql-server41relational-databasesblobfiletables-sql-servermd"></a>[FileTables &#40;SQL Server&#41;](../../relational-databases/blob/filetables-sql-server.md)  

La característica FileTable proporciona compatibilidad con el espacio de nombres de archivo de Windows y con las aplicaciones Windows para los datos de archivo almacenados en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. FileTable permite que una aplicación pueda integrar sus componentes de administración de datos y almacenamiento, así como proporcionar servicios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] integrados (incluidas la búsqueda de texto completo y la búsqueda semántica) en datos y metadatos no estructurados.  
  
 Es decir, ahora puede almacenar archivos y documentos en tablas especiales de FileTables denominadas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y tener acceso a ellos desde las aplicaciones Windows como si estuviesen almacenados en el sistema de archivos, sin efectuar cambios en las aplicaciones cliente.  
  
### <a name="remote-blob-store-40rbs41-40sql-server41relational-databasesblobremote-blob-store-rbs-sql-servermd"></a>[Almacén remoto de blobs &#40;RBS&#41; &#40;SQL Server&#41;](../../relational-databases/blob/remote-blob-store-rbs-sql-server.md)  

El almacén remoto de blobs (RBS) para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite a los administradores de bases de datos almacenar directamente objetos binarios grandes (blobs) en soluciones de almacenamiento estándar en lugar de directamente en el servidor. De este modo se ahorra una cantidad de espacio significativa y se evita malgastar los caros recursos de hardware de los servidores. RBS proporciona un conjunto de bibliotecas API que definen un modelo normalizado para que las aplicaciones accedan a los datos de los BLOB. RBS también incluye herramientas de mantenimiento, como la recolección de elementos no utilizados, para ayudar a administrar los datos BLOB remotos.  
  
 RBS se incluye en el disco de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pero no lo instala el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
  
