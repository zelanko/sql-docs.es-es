---
description: MSdistpublishers (Transact-SQL)
title: MSdistpublishers (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSdistpublishers
- MSdistpublishers_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSdistpublishers system table
ms.assetid: 31844099-4b33-4dc9-84b4-bac70aa82598
author: markingmyname
ms.author: maghan
ms.openlocfilehash: aa3f8872775f9d82a23d9ba2eb33a892696ca792
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551009"
---
# <a name="msdistpublishers-transact-sql"></a>MSdistpublishers (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  La tabla **MSdistpublishers** contiene una fila por cada publicador remoto que admite el distribuidor local. Esta tabla se almacena en la base de datos **msdb** .  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nombre del distribuidor publicador.|  
|**distribution_db**|**sysname**|El nombre de la base de datos de distribución.|  
|**working_directory**|**nvarchar(255)**|Nombre del directorio de trabajo utilizado para almacenar archivos de datos y de esquema para la publicación.|  
|**security_mode**|**int**|Modo de seguridad aplicado en el distribuidor:<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación.<br /><br /> **1** = autenticación de Windows.|  
|**Inicio**|**sysname**|Identificador de inicio de sesión para la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**password**|**nvarchar (524)**|Contraseña (cifrada) para la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**active**|**bit**|Indica si el publicador remoto está usando el distribuidor local.|  
|**trusted**|**bit**|Indica si el publicador remoto utiliza la misma contraseña que el distribuidor local:<br /><br /> **0** = se necesita una contraseña en el publicador remoto para conectarse al distribuidor.<br /><br /> **1** = no se necesita ninguna contraseña.|  
|**third_party**|**bit**|Indica si el publicador es una instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:<br /><br /> instalación de **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .** 1** = origen de datos heterogéneo.|  
|**publisher_type**|**sysname**|Tipo de publicador:<br /><br /> **MSSQLSERVER**  =  MSSQLSERVER [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicador.<br /><br /> **Oracle** = publicador estándar de Oracle.<br /><br /> **Puerta de enlace de Oracle** = publicador de puerta de enlace de Oracle.|  
|**storage_connection_string**|**nvarchar (779)**|Valor de Azure SQL Database cadena de conexión de almacenamiento.|  

  
## <a name="see-also"></a>Consulte también  
 [Tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
