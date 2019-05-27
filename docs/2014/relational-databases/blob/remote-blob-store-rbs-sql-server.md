---
title: Almacén remoto de blobs (RBS) (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.technology: filestream
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Remote Blob Store (RBS) [SQL Server]
- RBS (Remote Blob Store) [SQL Server]
ms.assetid: 31c947cf-53e9-4ff4-939b-4c1d034ea5b1
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 4379e0ff3ca534acd6ae130cbdf0f8acd2b6a81f
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/22/2019
ms.locfileid: "66009849"
---
# <a name="remote-blob-store-rbs-sql-server"></a>Remote Blob Store (RBS) (SQL Server)
  El almacén remoto de blobs RBS de[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es un componente complementario opcional que permite a los administradores de bases de datos almacenar directamente objetos binarios grandes en soluciones de almacenamiento de artículos en lugar de en el servidor de base de datos principal.  
  
 RBS se incluye en el disco de instalación de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] pero no lo instala el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Para obtener más información acerca de RBS, vea [RBS Resources](#rbsresources) en este tema.  
  
## <a name="benefits-of-rbs"></a>Ventajas de RBS  
 RBS proporciona las siguientes ventajas:  
  
### <a name="optimized-database-storage-and-performance"></a>Rendimiento y almacenamiento de base de datos optimizados  
 Si se almacenan los blobs en la base de datos, puede usarse una gran cantidad de espacio en los archivos y caros recursos del servidor. RBS transfiere eficazmente los blobs a la solución de almacenamiento especializada que prefiera y almacena las referencias a los mismos en la base de datos. Esto libera almacenamiento en el servidor para los datos estructurados y también recursos del servidor para las operaciones de base de datos.  
  
### <a name="efficient-management-of-blobs"></a>Una administración eficaz de los blobs  
 Varias características de RBS permiten una cómoda administración de los blobs almacenados:  
  
-   Los blobs se administran con transacciones duraderas de aislamiento atómico de coherencia (ACID).  
  
-   Los blobs se organizan en colecciones.  
  
-   Se incluyen la recolección de elementos no utilizados, la comprobación de la coherencia y otras funciones de mantenimiento.  
  
### <a name="standardized-api"></a>API normalizada  
 RBS define un conjunto de API que proporcionan un modelo de programación normalizado para que las aplicaciones obtengan acceso y modifiquen almacenes de blobs. Cada almacén de blobs puede especificar su propia biblioteca de proveedores, que se conecta a la biblioteca cliente de RBS y especifica cómo se almacenan los blobs y cómo se accede a ellos.  
  
 Varios proveedores de soluciones de almacenamiento han desarrollado proveedores RBS que se ajustan a estas API estándar y son compatibles con el almacenamiento de blobs en varias plataformas de almacenamiento.  
  
## <a name="rbs-requirements"></a>Requisitos de RBS  
 RBS requiere [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise para el servidor de base de datos principal en el que se almacenan los metadatos de los blobs. Sin embargo, si usa el proveedor FILESTREAM suministrado, puede almacenar los propios blobs en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Standard.  
  
 RBS incluye un proveedor FILESTREAM que permite usar RBS para almacenar los blobs en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si desea usar RBS para almacenar los blobs en una solución de almacenamiento diferente, tiene que usar un proveedor RBS de terceros desarrollado para dicha solución de almacenamiento o desarrollar un proveedor RBS personalizado con la API RBS. En [Codeplex](https://go.microsoft.com/fwlink/?LinkId=210190)hay disponible como recurso de aprendizaje un ejemplo de proveedor que almacena los blobs en el sistema de archivos NTFS.  
  
## <a name="rbs-security"></a>Seguridad de RBS  
 Cuando usa un proveedor personalizado para almacenar los blobs fuera de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], pueden estar disponibles para otros procesos que omiten el sistema de seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Asegúrese de que protege los blobs almacenados con opciones de cifrado y permisos apropiados para el medio de almacenamiento que use el proveedor personalizado.  
  
##  <a name="rbsresources"></a> Recursos de RBS  
 **Documentación de RBS**  
 La documentación de RBS se incluye en el paquete del programa de instalación de Windows. Si desea examinar la documentación de RBS sin instalarlo, puede ver la versión de [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] de la documentación [en línea en MSDN Library](https://go.microsoft.com/fwlink/?LinkId=210192).  
  
 **Notas RBS**  
 En las notas del producto "[Almacenamiento remoto de blobs](https://go.microsoft.com/fwlink/?LinkId=210422)", que pueden descargarse como documento de Microsoft Word, se proporciona información detallada acerca de la instalación y configuración de RBS.  
  
 **Ejemplos de RBS**  
 Los ejemplos de RBS disponibles en [Codeplex](https://go.microsoft.com/fwlink/?LinkId=210190) demuestran cómo desarrollar una aplicación de RBS y cómo desarrollar e instalar un proveedor de RBS personalizado.  
  
 **Blog de RBS**  
 En el [blog de RBS](https://go.microsoft.com/fwlink/?LinkId=210315) se proporciona información adicional para ayudarle a entender, implementar y mantener RBS.  
  
  
