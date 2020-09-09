---
description: MSpeer_originatorid_history (Transact-SQL)
title: MSpeer_originatorid_history (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSpeer_originatorid_history_TSQL
- MSpeer_originatorid_history
dev_langs:
- TSQL
helpviewer_keywords:
- MSpeer_originatorid_history
ms.assetid: c1f53d0f-4080-43ff-be38-2b10395c68c9
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 05ba5720a45bc8d448fe1ed24d6bdc950dcf290d
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545529"
---
# <a name="mspeer_originatorid_history-transact-sql"></a>MSpeer_originatorid_history (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contiene una fila para cada identificador de originador definido en la topología. Se incluyen los identificadores para los nodos que ya no están activos. La tabla se utiliza cuando se configura un nuevo nodo para la detección de conflictos con el fin de asegurarse de que no se ha utilizado todavía el identificador de originador especificado. Esta tabla se almacena en la base de datos de publicación. Para obtener más información sobre la detección de conflictos, vea [detección de conflictos en la replicación punto a punto](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|originator_publication|**sysname**|Publicación para la que se especificó el identificador de originador.|  
|originator_id|**int**|Número que identifica cada nodo de la topología para detectar conflictos.|  
|originator_node|**sysname**|Instancia del servidor para la que se especificó el identificador de originador.|  
|originator_db|**sysname**|Base de datos de publicación para la que se especificó el identificador de originador.|  
|originator_db_version|**int**|Identifica el número de versión de la base de datos de origen.|  
|originator_version|**int**|Identifica el número de versión del publicador.|  
|inserted_date|**datetime**|Fecha y hora en que la fila para el identificador de originador se insertó en esta tabla.|  
  
## <a name="see-also"></a>Consulte también  
 [Tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
