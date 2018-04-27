---
title: Establecer opciones de cifrado en servidores de destino | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQL Server Agent, encryption
- target servers [SQL Server], encryption
- multiserver environments [SQL Server], setting encryption options on target servers
ms.assetid: 1a9fd539-e166-4ea8-9f21-ac400ca74dee
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: bb1c59fe97fd336705dc72829885243ed30fb669
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="set-encryption-options-on-target-servers"></a>Establecer opciones de cifrado en servidores de destino
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> En [Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), la mayoría de las características de agente SQL Server son compatibles actualmente, aunque no todas. Vea [Diferencias de T-SQL en Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para obtener más información.

Si no puede usar un certificado para comunicaciones cifradas con Capa de sockets seguros (SSL) entre servidores principales y alguno o todos los servidores de destino, pero desea cifrar el canal entre ellos, configure el servidor de destino para usar el nivel de seguridad necesario.  
  
Para configurar el nivel de seguridad necesario para el canal de comunicación específico entre un servidor maestro y un servidor de destino, establezca la subclave del Registro del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\**\<*nombre_instancia*>**\SQLServerAgent\MsxEncryptChannelOptions(REG_DWORD)** del servidor de destino en uno de los siguientes valores. El valor de \<*nombre_de_instancia*> es *MSSQL.***n*. Por ejemplo, **MSSQL.1** o **MSSQL.3**.  
  
|Valor|Description|  
|---------|---------------|  
|**0**|Deshabilita el cifrado entre este servidor de destino y el servidor maestro. Elija esta opción únicamente cuando el canal entre el servidor de destino y el servidor principal se ha protegido por otros medios.|  
|**1**|Habilita el cifrado solo entre este servidor de destino y el servidor principal, pero no se requiere validación de certificados.|  
|**2**|Habilita el cifrado SSL y la validación de certificados completos entre este servidor de destino y el servidor principal. Ésta es la configuración predeterminada. A menos que tenga una razón concreta para elegir un valor diferente, se recomienda no modificarlo.|  
  
Si se especifica **1** o **2** , debe tener habilitado SSL en los servidores maestro y de destino. Si se especifica **2** , debe tener además un certificado debidamente firmado presente en el servidor maestro.  
  
> [!CAUTION]  
> [!INCLUDE[ssNoteRegistry](../../includes/ssnoteregistry_md.md)]  
  
## <a name="see-also"></a>Ver también  
[Cómo habilitar conexiones cifradas en el motor de base de datos (Administrador de configuración de SQL Server)](http://msdn.microsoft.com/en-us/e1e55519-97ec-4404-81ef-881da3b42006)  
  
