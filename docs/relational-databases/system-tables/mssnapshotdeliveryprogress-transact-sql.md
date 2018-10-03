---
title: MSsnapshotdeliveryprogress (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- MSsnapshotdeliveryprogress_TSQL
- MSsnapshotdeliveryprogress
dev_langs:
- TSQL
helpviewer_keywords:
- MSsnapshotdeliveryprogress system table
ms.assetid: 9164bfe2-6fc4-4b52-946a-09ea3cf67041
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 59be6e8f6faaded5ffb78f2e7dd8fecb4371ed52
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47720953"
---
# <a name="mssnapshotdeliveryprogress-transact-sql"></a>MSsnapshotdeliveryprogress (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El **MSsnapshotdeliveryprogress** tabla se utiliza para realizar un seguimiento de los archivos que se han entregado correctamente al suscriptor cuando se aplica una instantánea. Estos datos se utilizan para reanudar la entrega de archivos en caso de que el Agente de mezcla no entregue todos los archivos durante la sesión. De esta forma, se evita que aquellos archivos que ya se han entregado se vuelvan a entregar la siguiente vez que se ejecute el Agente de mezcla. Esta tabla se almacena en el suscriptor en la base de datos de suscripciones.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**session_token**|**nvarchar(260)**|Identifica la ruta de acceso a la carpeta de instantáneas desde la que se ha entregado correctamente el archivo. Para las publicaciones que utilizan filtros con parámetros, la cadena **dynsnap** se anexará al valor.|  
|**progress_token_hash**|**int**|Un valor hash generado según el valor de *progress_token* que se usa mejorar la eficacia de la búsqueda para un determinado *progress_token* valor.|  
|**progress_token**|**nvarchar(500)**|Identifica un archivo entregado correctamente, donde el valor es una combinación del nombre y la ruta de acceso del archivo.|  
|**progress_timestamp**|**datetime**|El **datetime** valor que indica cuándo se ha entregado correctamente un archivo de instantánea.|  
  
## <a name="see-also"></a>Vea también  
 [Las tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
