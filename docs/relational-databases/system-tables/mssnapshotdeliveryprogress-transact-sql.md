---
title: MSsnapshotdeliveryprogress (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSsnapshotdeliveryprogress_TSQL
- MSsnapshotdeliveryprogress
dev_langs:
- TSQL
helpviewer_keywords:
- MSsnapshotdeliveryprogress system table
ms.assetid: 9164bfe2-6fc4-4b52-946a-09ea3cf67041
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: f4cd21fcc026e48c0e0f4ca68ada16bf55855662
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2020
ms.locfileid: "85889391"
---
# <a name="mssnapshotdeliveryprogress-transact-sql"></a>MSsnapshotdeliveryprogress (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  La tabla **MSsnapshotdeliveryprogress** se utiliza para realizar el seguimiento de los archivos que se han entregado correctamente al suscriptor cuando se aplica una instantánea. Estos datos se utilizan para reanudar la entrega de archivos en caso de que el Agente de mezcla no entregue todos los archivos durante la sesión. De esta forma, se evita que aquellos archivos que ya se han entregado se vuelvan a entregar la siguiente vez que se ejecute el Agente de mezcla. Esta tabla se almacena en el suscriptor en la base de datos de suscripciones.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**session_token**|**nvarchar(260)**|Identifica la ruta de acceso a la carpeta de instantáneas desde la que se ha entregado correctamente el archivo. En el caso de las publicaciones que utilizan filtros con parámetros, la cadena **dynsnap** se anexará al valor.|  
|**progress_token_hash**|**int**|Valor hash generado basándose en el valor de *progress_token* que se usa para mejorar la eficacia de la búsqueda de un valor de *progress_token* determinado.|  
|**progress_token**|**nvarchar (500)**|Identifica un archivo entregado correctamente, donde el valor es una combinación del nombre y la ruta de acceso del archivo.|  
|**progress_timestamp**|**datetime**|Valor de **fecha y hora** que indica cuándo se entregó correctamente un archivo de instantánea.|  
  
## <a name="see-also"></a>Consulte también  
 [Tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
