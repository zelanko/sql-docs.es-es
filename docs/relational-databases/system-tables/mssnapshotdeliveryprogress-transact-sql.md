---
title: MSsnapshotdeliveryprogress (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- MSsnapshotdeliveryprogress_TSQL
- MSsnapshotdeliveryprogress
dev_langs:
- TSQL
helpviewer_keywords:
- MSsnapshotdeliveryprogress system table
ms.assetid: 9164bfe2-6fc4-4b52-946a-09ea3cf67041
caps.latest.revision: 30
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 0989999080b57bf2f78b6a297df29a0ee8a32f35
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="mssnapshotdeliveryprogress-transact-sql"></a>MSsnapshotdeliveryprogress (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El **MSsnapshotdeliveryprogress** tabla sirve para realizar un seguimiento de los archivos que se han entregado correctamente al suscriptor cuando se aplica una instantánea. Estos datos se utilizan para reanudar la entrega de archivos en caso de que el Agente de mezcla no entregue todos los archivos durante la sesión. De esta forma, se evita que aquellos archivos que ya se han entregado se vuelvan a entregar la siguiente vez que se ejecute el Agente de mezcla. Esta tabla se almacena en el suscriptor en la base de datos de suscripciones.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**session_token**|**nvarchar(260)**|Identifica la ruta de acceso a la carpeta de instantáneas desde la que se ha entregado correctamente el archivo. Para las publicaciones que utilizan filtros con parámetros, la cadena **dynsnap** se anexará al valor.|  
|**progress_token_hash**|**int**|Un valor hash generado según el valor de *progress_token* que se usa mejorar la eficacia de la búsqueda para un determinado *progress_token* valor.|  
|**progress_token**|**nvarchar(500)**|Identifica un archivo entregado correctamente, donde el valor es una combinación del nombre y la ruta de acceso del archivo.|  
|**progress_timestamp**|**datetime**|El **datetime** valor que indica si se ha entregado correctamente un archivo de instantánea.|  
  
## <a name="see-also"></a>Vea también  
 [Tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
