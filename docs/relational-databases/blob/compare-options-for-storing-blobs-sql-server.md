---
title: Comparar opciones para almacenar objetos Blob (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
ms.assetid: 6038697b-36a9-49e8-a02a-2ad9e2e60e5a
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 20d392d5019bf643654bb3a0a6989f882a05b671
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65094226"
---
# <a name="compare-options-for-storing-blobs-sql-server"></a>Comparar opciones para almacenar objetos Blob (SQL Server)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Explica y compara las opciones que están disponibles para almacenar archivos y documentos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

## <a name="Expectations"></a> Almacenamiento de archivos en la base de datos - Ventajas y expectativas

Un porcentaje alto de los datos empresariales no se estructuran por naturaleza y se suelen almacenar como archivos y documentos en los sistemas de archivos. Las aplicaciones que tienen acceso a los archivos a través de las API de Windows generan, administran y consumen la mayor parte de los datos. Las empresas suelen mantener estos datos en el sistema de archivos, mientras que almacenan los metadatos relacionados de los archivos en una base de datos relacional.

Integrar los datos no estructurados en la base de datos relacional proporciona las siguientes ventajas:

- Capacidades de almacenamiento integrado y administración de datos como la copia de seguridad.
- Servicios integrados como la búsqueda de texto completo y la búsqueda semántica en datos y metadatos.
- Facilidad de administración y administración de directivas en datos no estructurados.

Por lo general, no ha sido muy cómodo almacenar los datos no estructurados en una base de datos relacional. No ha sido práctico volver a escribir aplicaciones establecidas (como Microsoft Word o Adobe Reader) para que interactúen mediante las API de bases de datos relacionales. Estas aplicaciones esperan que se acceda a los datos a través de las API de Windows. Las aplicaciones presentan los siguientes requisitos:

- Las aplicaciones Windows no tienen en cuenta las transacciones de la base de datos y no las necesitan.
- Las aplicaciones Windows requieren compatibilidad con las API del sistema de archivos para los datos de archivos y directorios.

Años atrás, SQL Server no ofrecía ninguna forma de almacenar datos no estructurados en una base de datos relacional, pero en la actualidad sí proporciona varios métodos para almacenarlos.

## <a name="Filestream"></a> FILESTREAM

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ya incluye la característica FILESTREAM, que proporciona almacenamiento, administración y transmisión de datos eficaces de los datos no estructurados almacenados como archivos en el sistema de archivos. Sin embargo, una solución FILESTREAM requiere la programación personalizada y no satisface el requisito de compatibilidad completa de las aplicaciones Windows descrito anteriormente.

## <a name="FileTables"></a> FileTables

La característica FileTable se basa en las capacidades de FILESTREAM existentes. La característica FileTable permite a los clientes empresariales almacenar datos de archivos no estructurados y jerarquías de directorios en una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta característica aborda los requisitos de acceso no transaccional y compatibilidad de aplicaciones Windows de los datos basados en archivos.

## <a name="CompareFileTable"></a> Comparar FILESTREAM y FileTable

|Característica|Servidor de archivos y solución de base de datos|Solución de FILESTREAM|Solución de FileTable|
|:------|:--------------------------------|:------------------|:-----------------|
|**Un solo artículo para tareas de administración**|No|Sí|**Sí**|
|**Un solo conjunto de servicios**: búsquedas, informes, consultas, etc.|No|Sí|**Sí**|
|**Modelo de seguridad integrada**|No|Sí|**Sí**|
|**Actualizaciones en contexto de datos FILESTREAM**|Sí|No|**Sí**|
|**Jerarquía de archivos y de directorios que se mantiene en la base de datos**|No|No|**Sí**|
|**Compatibilidad con aplicaciones Windows**|Sí|No|**Sí**|
|**Acceso relacional a los atributos de archivo**|No|No|**Sí**|

## <a name="CompareRBS"></a> Comparar FILESTREAM y el almacén remoto de BLOBS (RBS)

Otra opción para almacenar datos no estructurados conlleva el uso de un Almacén remoto de blobs (RBS). Para obtener más información, vea [Almacén remoto de blobs (RBS) (SQL Server)](remote-blob-store-rbs-sql-server.md).

## <a name="more"></a> Más información

[FILESTREAM &#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md)  
[FileTables &#40;SQL Server&#41;](../../relational-databases/blob/filetables-sql-server.md)  
[Almacén remoto de blobs &#40;RBS&#41; &#40;SQL Server&#41;](../../relational-databases/blob/remote-blob-store-rbs-sql-server.md)
