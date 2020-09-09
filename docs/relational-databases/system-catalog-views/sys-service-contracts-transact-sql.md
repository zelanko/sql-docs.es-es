---
description: sys.service_contracts (Transact-SQL)
title: Sys. service_contracts (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- service_contracts_TSQL
- sys.service_contracts_TSQL
- sys.service_contracts
- service_contracts
dev_langs:
- TSQL
helpviewer_keywords:
- sys.service_contracts catalog view
ms.assetid: 787dd47e-4210-439d-9c4a-57a727a0dbd8
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 00e98ef129f6430a644b1a688e838fa51c5b6ae5
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/08/2020
ms.locfileid: "89539558"
---
# <a name="sysservice_contracts-transact-sql"></a>sys.service_contracts (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Esta vista de catálogo contiene una fila por cada contrato en la base de datos.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nombre del contrato, único en la base de datos. No acepta valores NULL.|  
|**service_contract_id**|**int**|Identificador del contrato. No acepta valores NULL.|  
|**principal_id**|**int**|Identificador de la base de datos de la entidad de seguridad propietaria del contrato. Acepta valores NULL.|  
  
## <a name="permissions"></a>Permisos  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
  
