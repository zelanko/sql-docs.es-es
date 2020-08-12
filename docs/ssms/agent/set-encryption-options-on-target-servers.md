---
title: Establecer opciones de cifrado en servidores de destino
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, encryption
- target servers [SQL Server], encryption
- multiserver environments [SQL Server], setting encryption options on target servers
ms.assetid: 1a9fd539-e166-4ea8-9f21-ac400ca74dee
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: ee53a4f973537dad629a24bb442e8a1076eebd11
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85644531"
---
# <a name="set-encryption-options-on-target-servers"></a>Establecer opciones de cifrado en servidores de destino
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> En [Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), la mayoría de las características de agente SQL Server son compatibles actualmente, aunque no todas. Vea [Diferencias de T-SQL en Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para obtener más información.

Si no puede usar un certificado para comunicaciones cifradas con la Seguridad de la capa de transporte (TLS), anteriormente conocida como Capa de sockets seguros (SSL), entre servidores maestros y alguno o todos los servidores de destino, pero quiere cifrar el canal entre ellos, configure el servidor de destino para usar el nivel de seguridad necesario.  
  
Para configurar el nivel de seguridad adecuado necesario para un canal de comunicación específico entre un servidor maestro y un servidor de destino, establezca la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]subclave del Registro del Agente **\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\** \<*instance_name*> **\SQLServerAgent\MsxEncryptChannelOptions(REG_DWORD)** del servidor de destino en uno de los valores siguientes. El valor de \<*instance_name*> es **MSSQL.** _n_. Por ejemplo, **MSSQL.1** o **MSSQL.3**.  
  
|Value|Descripción|  
|---------|---------------|  
|**0**|Deshabilita el cifrado entre este servidor de destino y el servidor maestro. Elija esta opción únicamente cuando el canal entre el servidor de destino y el servidor principal se ha protegido por otros medios.|  
|**1**|Habilita el cifrado solo entre este servidor de destino y el servidor principal, pero no se requiere validación de certificados.|  
|**2**|Habilita el cifrado TLS y la validación de certificados completos entre este servidor de destino y el servidor maestro. Esta es la configuración predeterminada. A menos que tenga una razón concreta para elegir un valor diferente, se recomienda no modificarlo.|  
  
Si se especifica **1** o **2**, debe tener habilitado TLS en los servidores maestro y de destino. Si se especifica **2** , debe tener además un certificado debidamente firmado presente en el servidor maestro.  
  
> [!CAUTION]  
> [!INCLUDE[ssNoteRegistry](../../includes/ssnoteregistry-md.md)]  
  
## <a name="see-also"></a>Consulte también  
[Cómo: Habilitar conexiones cifradas en el motor de base de datos (Administrador de configuración de SQL Server)](https://msdn.microsoft.com/e1e55519-97ec-4404-81ef-881da3b42006)  
  
