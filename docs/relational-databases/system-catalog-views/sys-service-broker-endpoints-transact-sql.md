---
title: sys.service_broker_endpoints (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.service_broker_endpoints_TSQL
- service_broker_endpoints
- service_broker_endpoints_TSQL
- sys.service_broker_endpoints
dev_langs:
- TSQL
helpviewer_keywords:
- sys.service_broker_endpoints catalog view
ms.assetid: 6979ec9b-0043-411e-aafb-0226fa26c5ba
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4bb8361040ebdaf9b7e7dc98aab3e40ea9152c4b
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/03/2018
---
# <a name="sysservicebrokerendpoints-transact-sql"></a>sys.service_broker_endpoints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Esta vista de catálogo contiene una fila por cada extremo de Service Broker. Para cada fila de esta vista, no hay una fila correspondiente con el mismo **endpoint_id** en el **sys.tcp_endpoints** vista que contiene los metadatos de configuración de TCP. TCP es el único protocolo permitido para Service Broker.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**\<hereda columnas >**|**--**|Hereda columnas de [sys.endpoints &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-endpoints-transact-sql.md).|  
|**is_message_forwarding_enabled**|**bit**|El extremo admite el reenvío de mensajes. Esto se establece inicialmente en **0** (deshabilitado). No acepta valores NULL.|  
|**message_forwarding_size**|**int**|El número máximo de megabytes de **tempdb** permite el espacio que se utilizará para los mensajes que se reenvían. Esto se establece inicialmente en **10**. No acepta valores NULL.|  
|**connection_auth**|**tinyint**|Tipo de autenticación de la conexión necesario para las conexiones con este extremo; uno de los siguientes:<br /><br /> **1** - NTLM<br /><br /> **2** - KERBEROS<br /><br /> **3** -NEGOCIAR<br /><br /> **4** -CERTIFICADO<br /><br /> **5** -NTLM, CERTIFICADOS<br /><br /> **6** -KERBEROS, CERTIFICADO<br /><br /> **7** -NEGOTIATE, CERTIFICADOS<br /><br /> **8** -CERTIFICADO, NTLM<br /><br /> **9** -CERTIFICADO, KERBEROS<br /><br /> **10** -CERTIFICADO, NEGOTIATE<br /><br /> No acepta valores NULL.|  
|**connection_auth_desc**|**nvarchar(60)**|Descripción del tipo de autenticación de conexión requerido para conexiones a este extremo. Es una de las opciones siguientes:<br /><br /> NTLM<br /><br /> KERBEROS<br /><br /> NEGOTIATE<br /><br /> CERTIFICATE<br /><br /> NTLM, CERTIFICATE<br /><br /> KERBEROS, CERTIFICATE<br /><br /> NEGOTIATE, CERTIFICATE<br /><br /> CERTIFICATE, NTLM<br /><br /> CERTIFICATE, KERBEROS<br /><br /> CERTIFICATE, NEGOTIATE<br /><br /> ACEPTA VALORES NULL.|  
|**certificate_id**|**int**|Identificador del certificado utilizado para la autenticación, si lo hay.<br /><br /> 0 = Se está utilizando la Autenticación de Windows.|  
|**encryption_algorithm**|**tinyint**|Algoritmo de cifrado. Éstos son los valores posibles con sus descripciones y las correspondientes opciones de DDL.<br /><br /> **0** : NINGUNO. Opción DDL correspondiente: deshabilitado.<br /><br /> **1** :  RC4. Opción DDL correspondiente: {necesario &#124; Necesita el algoritmo RC4}.<br /><br /> **2** : AES. Opción DDL correspondiente: requiere el algoritmo AES.<br /><br /> **3** : NONE, RC4. Opción DDL correspondiente: {Supported &#124; Se admite el algoritmo RC4}.<br /><br /> **4** : NINGUNO, AES. Opción DDL correspondiente: admite el algoritmo AES.<br /><br /> **5** : RC4, AES. Opción DDL correspondiente: requiere el algoritmo RC4 AES.<br /><br /> **6** : AES, RC4. Opción DDL correspondiente: requiere el algoritmo AES RC4.<br /><br /> **7** : NONE, RC4, AES. Opción DDL correspondiente: admite el algoritmo RC4 AES.<br /><br /> **8** : NINGUNO, AES, RC4. Opción DDL correspondiente: admite el algoritmo AES RC4.<br /><br /> No acepta valores NULL.|  
|**encryption_algorithm_desc**|**nvarchar(60)**|Descripción del algoritmo de cifrado. Los valores posibles y sus opciones de DDL correspondientes se enumeran a continuación:<br /><br /> Ninguno: deshabilitado<br /><br /> RC4: {necesario &#124; Se necesita el algoritmo RC4}<br /><br /> AES: Se necesita el algoritmo AES<br /><br /> NONE, RC4: {admite &#124; Se admite el algoritmo RC4}<br /><br /> Ninguno, AES: Admite el algoritmo AES<br /><br /> RC4, AES: Requiere el algoritmo RC4 AES<br /><br /> AES, RC4: Se necesita el algoritmo AES RC4<br /><br /> NONE, RC4, AES: Admite el algoritmo RC4 AES<br /><br /> Ninguno, AES, RC4: Admite el algoritmo AES RC4<br /><br /> ACEPTA VALORES NULL.|  
  
## <a name="remarks"></a>Comentarios  
  
> [!NOTE]  
>  El algoritmo RC4 se admite únicamente por razones de compatibilidad con versiones anteriores. El material nuevo solo se puede cifrar con RC4 o RC4_128 cuando la base de datos tenga el nivel de compatibilidad 90 o 100. (No se recomienda). Use un algoritmo más reciente como uno de los algoritmos AES en su lugar. En [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] y versiones posteriores, el material cifrado con RC4 o RC4_128 se puede descifrar en cualquier nivel de compatibilidad.  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [ALTER ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/alter-endpoint-transact-sql.md)   
 [Crear punto de conexión &#40; Transact-SQL &#41;](../../t-sql/statements/create-endpoint-transact-sql.md)  
  
  
