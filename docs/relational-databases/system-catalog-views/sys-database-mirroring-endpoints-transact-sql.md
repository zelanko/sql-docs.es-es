---
title: Sys.database_mirroring_endpoints (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.database_mirroring_endpoints_TSQL
- database_mirroring_endpoints
- sys.database_mirroring_endpoints
- database_mirroring_endpoints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- database mirroring [SQL Server], endpoint
- HADR [SQL Server], endpoint
- database mirroring [SQL Server], catalog views
- sys.database_mirroring_endpoints catalog view
ms.assetid: f2285199-97ad-473c-a52d-270044dd862b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c4a791f5d47382e78ce9bbfe34d939cffc273515
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47734603"
---
# <a name="sysdatabasemirroringendpoints-transact-sql"></a>sys.database_mirroring_endpoints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una fila para el extremo de creación de reflejo de la base de datos de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  El extremo de reflejo de la base de datos admite tanto las sesiones entre asociados de creación de reflejo de la base de datos y los testigos y sesiones entre la réplica principal de un grupo de disponibilidad AlwaysOn y sus réplicas secundarias.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**\<hereda columnas >**|—|Hereda columnas de **sys.endpoints** (para obtener más información, consulte [sys.endpoints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-endpoints-transact-sql.md)).|  
|**Rol**|**tinyint**|Rol de creación de reflejo, uno de los siguientes:<br /><br /> **0** = ninguno<br /><br /> **1** = partner<br /><br /> **2** = testigo<br /><br /> **3** = all<br /><br /> Nota: Este valor solo es relevante para la creación de reflejo de base de datos.|  
|**role_desc**|**nvarchar(60)**|Descripción del rol de creación de reflejo, uno de los siguientes:<br /><br /> **NONE**<br /><br /> **PARTNER**<br /><br /> **TESTIGO**<br /><br /> **ALL**<br /><br /> Nota: Este valor solo es relevante para la creación de reflejo de base de datos.|  
|**is_encryption_enabled**|**bit**|**1** significa que el cifrado está habilitado.<br /><br /> **0** significa que el cifrado está deshabilitado.|  
|**connection_auth**|**tinyint**|Tipo de autenticación de la conexión necesario para las conexiones con este extremo; uno de los siguientes:<br /><br /> **1** -NTLM<br /><br /> **2** -KERBEROS<br /><br /> **3** -NEGOCIAR<br /><br /> **4** -CERTIFICADO<br /><br /> **5** -NTLM, EL CERTIFICADO<br /><br /> **6** -KERBEROS, CERTIFICADO<br /><br /> **7** -NEGOTIATE, CERTIFICADOS<br /><br /> **8** -CERTIFICADO, NTLM<br /><br /> **9** -CERTIFICADO, KERBEROS<br /><br /> **10** -CERTIFICADO, NEGOTIATE|  
|**connection_auth_desc**|**Nvarchar (60)**|Descripción del tipo de autenticación necesario para las conexiones con este extremo; uno de los siguientes:<br /><br /> NTLM<br /><br /> KERBEROS<br /><br /> NEGOTIATE<br /><br /> CERTIFICATE<br /><br /> NTLM, CERTIFICATE<br /><br /> KERBEROS, CERTIFICATE<br /><br /> NEGOTIATE, CERTIFICATE<br /><br /> CERTIFICATE, NTLM<br /><br /> CERTIFICATE, KERBEROS<br /><br /> CERTIFICATE, NEGOTIATE|  
|**certificate_id**|**int**|Identificador del certificado utilizado para la autenticación, si lo hay.<br /><br /> 0 = Se está utilizando la Autenticación de Windows.|  
|**encryption_algorithm**|**tinyint**|Algoritmo de cifrado, uno de los siguientes:<br /><br /> **0** : NONE<br /><br /> **1** – RC4<br /><br /> **2** : AES<br /><br /> **3** : NONE, RC4<br /><br /> **4** : NINGUNO, AES<br /><br /> **5** : RC4, AES<br /><br /> **6** : AES, RC4<br /><br /> **7** : NONE, RC4, AES<br /><br /> **8** : NINGUNO, AES, RC4|  
|**encryption_algorithm_desc**|**nvarchar(60)**|Descripción del algoritmo de cifrado, uno de los siguientes:<br /><br /> Ninguno<br /><br /> RC4<br /><br /> AES<br /><br /> NONE, RC4<br /><br /> NONE, AES<br /><br /> RC4, AES<br /><br /> AES, RC4<br /><br /> NONE, RC4, AES<br /><br /> NONE, AES, RC4|  
  
## <a name="remarks"></a>Comentarios  
  
> [!NOTE]  
>  El algoritmo RC4 se admite únicamente por razones de compatibilidad con versiones anteriores. El material nuevo solo se puede cifrar con RC4 o RC4_128 cuando la base de datos tenga el nivel de compatibilidad 90 o 100. (No se recomienda). Use un algoritmo más reciente como uno de los algoritmos AES en su lugar. En [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] y versiones posteriores, el material cifrado con RC4 o RC4_128 se puede descifrar en cualquier nivel de compatibilidad.  
  
## <a name="permissions"></a>Permisos  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Especifique la dirección URL del extremo al agregar o modificar una réplica de disponibilidad &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/specify-endpoint-url-adding-or-modifying-availability-replica.md)   
 [sys.availability_replicas &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-availability-replicas-transact-sql.md)   
 [Sys.database_mirroring &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-mirroring-transact-sql.md)   
 [sys.database_mirroring_witnesses &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)   
 [El punto de conexión de creación de reflejo de la base de datos &#40;SQL Server&#41;](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)   
 [Preguntas frecuentes sobre consultas del catálogo de sistema de SQL Server](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
