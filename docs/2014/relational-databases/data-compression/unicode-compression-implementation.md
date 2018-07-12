---
title: Implementación de la compresión Unicode | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Unicode data compression
- compression [SQL Server], Unicode data
ms.assetid: 44e69e60-9b35-43fe-b9c7-8cf34eaea62a
caps.latest.revision: 7
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 216e2278418747a713575c165f14390c7b785e71
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37156342"
---
# <a name="unicode-compression-implementation"></a>Implementación de la compresión Unicode
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa una implementación del algoritmo del esquema de compresión estándar para Unicode (SCSU) para comprimir los valores Unicode que están almacenados en objetos comprimidos de fila o página. Para estos objetos comprimidos, la compresión Unicode es automática para columnas `nchar(n)` y `nvarchar(n)`. [!INCLUDE[ssDE](../../includes/ssde-md.md)] almacena los datos Unicode como 2 bytes, independientemente de la configuración regional. Esto se denomina codificación UCS-2. Para algunas configuraciones regionales, la implementación de la compresión SCSU en SQL Server puede ahorrar hasta el 50% de espacio de almacenamiento.  
  
## <a name="supported-data-types"></a>Tipos de datos admitidos  
 La compresión Unicode admite los tipos de datos `nchar(n)` y `nvarchar(n)` de longitud fija. Los valores de datos que no están almacenados de forma consecutiva o en columnas `nvarchar(max)` no se comprimen.  
  
> [!NOTE]  
>  No se admite la compresión Unicode para `nvarchar(max)` incluso si se almacena en la fila de datos. Sin embargo, este tipo de datos puede seguir beneficiándose de la compresión de página.  
  
## <a name="upgrading-from-earlier-versions-of-sql-server"></a>Actualizar de versiones anteriores de SQL Server  
 Cuando una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se actualiza a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], los cambios relacionados con la compresión Unicode no se llevan a cabo en ningún objeto de base de datos, tanto si está comprimido como si no lo está. Una vez actualizada la base de datos, los objetos se ven afectados de la siguiente forma:  
  
-   Si el objeto no está comprimido, no se realiza ningún cambio y sigue funcionando como lo hacía anteriormente.  
  
-   Los objetos comprimidos de fila o página siguen funcionando como lo hacían anteriormente. Los datos sin comprimir permanecen sin comprimir hasta que se actualiza su valor.  
  
-   Las nuevas filas que se insertan en una tabla comprimida de fila o página se comprimen con la compresión Unicode.  
  
    > [!NOTE]  
    >  Para aprovechar al máximo las ventajas de la compresión Unicode, el objeto se debe regenerar con la compresión de página o fila.  
  
## <a name="how-unicode-compression-affects-data-storage"></a>Cómo afecta la compresión Unicode al almacenamiento de datos  
 Cuando un índice se crea o regenera, o bien cuando un valor se cambia en una tabla que se comprimió con compresión de fila o página, el índice o el valor afectado se almacena comprimido solo si su tamaño comprimido es menor que su tamaño actual. De este modo se evita que las filas de una tabla o índice aumenten de tamaño debido a la compresión Unicode.  
  
 El espacio de almacenamiento que la compresión ahorra depende de las características de los datos que se vayan a comprimir y la configuración regional de dichos datos. En la tabla siguiente se enumeran los ahorros de espacio que se pueden conseguir para diferentes configuraciones regionales.  
  
|Configuración regional|Porcentaje de compresión|  
|------------|-------------------------|  
|Inglés|50%|  
|German|50%|  
|Hindi|50%|  
|Turco|48 %|  
|Vietnamita|39 %|  
|Japonés|15 %|  
  
## <a name="see-also"></a>Vea también  
 [Comprimir datos](data-compression.md)   
 [sp_estimate_data_compression_savings &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-estimate-data-compression-savings-transact-sql)   
 [Implementación de la compresión de página](page-compression-implementation.md)   
 [sys.dm_db_persisted_sku_features &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-persisted-sku-features-transact-sql)  
  
  
