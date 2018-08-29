---
title: Sys.remote_logins (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.remote_logins_TSQL
- remote_logins
- remote_logins_TSQL
- sys.remote_logins
dev_langs:
- TSQL
helpviewer_keywords:
- sys.remote_logins catalog view
ms.assetid: 38477e91-d084-4df7-b1de-b930c5580189
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 7f4c403c86373043cd98ebec8121c696c384be4d
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43023983"
---
# <a name="sysremotelogins-transact-sql"></a>sys.remote_logins (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve una fila por cada asignación de inicio de sesión remoto. Esta vista de catálogo se utiliza para asignar inicios de sesión locales entrantes originados en el servidor correspondiente para un inicio de sesión local real.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**server_id**|**int**|Id. del servidor en **sys.servers**. Este nombre es suministrado por la conexión desde el servidor "remoto".|  
|**remote_name**|**sysname**|Nombre de inicio de sesión que suministra la conexión para su asignación. Si el valor es NULL, se utiliza el nombre de inicio de sesión especificado en la conexión.|  
|**local_principal_id**|**int**|Id. de la entidad de seguridad del servidor a la que se asigna el inicio de sesión. Si el valor es 0, el inicio de sesión remoto se asigna al inicio de sesión con el mismo nombre.|  
|**modify_date**|**datetime**|Fecha en que se cambió el inicio de sesión vinculado por última vez.|  
  
## <a name="permissions"></a>Permisos  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Vistas de catálogo de servidores vinculados &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/linked-servers-catalog-views-transact-sql.md)   
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
