---
title: Establecer opciones de cifrado en servidores de destino | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, encryption
- target servers [SQL Server], encryption
- multiserver environments [SQL Server], setting encryption options on target servers
ms.assetid: 1a9fd539-e166-4ea8-9f21-ac400ca74dee
author: stevestein
ms.author: sstein
ms.openlocfilehash: cd10d2e05e59015542f41cc123de993e6128f9f6
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85067564"
---
# <a name="set-encryption-options-on-target-servers"></a>Establecer opciones de cifrado en servidores de destino
  Si no puede usar un certificado para comunicaciones cifradas con Capa de sockets seguros (SSL) entre servidores principales y alguno o todos los servidores de destino, pero desea cifrar el canal entre ellos, configure el servidor de destino para usar el nivel de seguridad necesario.  
  
 Para configurar el nivel de seguridad adecuado necesario para un canal de comunicación específico entre un servidor maestro y un servidor de destino, establezca la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] subclave del registro del agente **\ HKEY_LOCAL_MACHINE \software\microsoft\microsoft \\ SQL Server** \<*instance_name*> **\SQLServerAgent\MsxEncryptChannelOptions (REG_DWORD)** en el servidor de destino en uno de los valores siguientes. El valor de \<*instance_name*> es **MSSQL.** _n_. Por ejemplo, **MSSQL.1** o **MSSQL.3**.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**0**|Deshabilita el cifrado entre este servidor de destino y el servidor maestro. Elija esta opción únicamente cuando el canal entre el servidor de destino y el servidor principal se ha protegido por otros medios.|  
|**1**|Habilita el cifrado solo entre este servidor de destino y el servidor principal, pero no se requiere validación de certificados.|  
|**2**|Habilita el cifrado SSL y la validación de certificados completos entre este servidor de destino y el servidor principal. Esta es la configuración predeterminada. A menos que tenga una razón concreta para elegir un valor diferente, se recomienda no modificarlo.|  
  
 Si se especifica **1** o **2** , debe tener habilitado SSL en los servidores maestro y de destino. Si se especifica **2** , debe tener además un certificado debidamente firmado presente en el servidor maestro.  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteRegistry](../../includes/ssnoteregistry-md.md)]  
  
## <a name="see-also"></a>Consulte también  
 [Habilitar conexiones cifradas en el motor de base de datos &#40;Administrador de configuración de SQL Server&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)  
  
  
