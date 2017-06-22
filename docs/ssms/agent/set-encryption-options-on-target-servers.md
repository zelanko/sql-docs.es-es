---
title: Establecer opciones de cifrado en servidores de destino | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Agent, encryption
- target servers [SQL Server], encryption
- multiserver environments [SQL Server], setting encryption options on target servers
ms.assetid: 1a9fd539-e166-4ea8-9f21-ac400ca74dee
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 746d0d91d4625c6daad4a4133c0a4481ef85f7d9
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="set-encryption-options-on-target-servers"></a>Establecer opciones de cifrado en servidores de destino
Si no puede usar un certificado para comunicaciones cifradas con Capa de sockets seguros (SSL) entre servidores principales y alguno o todos los servidores de destino, pero desea cifrar el canal entre ellos, configure el servidor de destino para usar el nivel de seguridad necesario.  
  
Para configurar el nivel de seguridad necesario para el canal de comunicación específico entre un servidor maestro y un servidor de destino, establezca la subclave del Registro del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\**\<*nombre_instancia*>**\SQLServerAgent\MsxEncryptChannelOptions(REG_DWORD)** del servidor de destino en uno de los siguientes valores. El valor de \<*nombre_instancia*> es **MSSQL.***n*. Por ejemplo, **MSSQL.1** o **MSSQL.3**.  
  
|Value|Descripción|  
|---------|---------------|  
|**0**|Deshabilita el cifrado entre este servidor de destino y el servidor maestro. Elija esta opción únicamente cuando el canal entre el servidor de destino y el servidor principal se ha protegido por otros medios.|  
|**1**|Habilita el cifrado solo entre este servidor de destino y el servidor principal, pero no se requiere validación de certificados.|  
|**2**|Habilita el cifrado SSL y la validación de certificados completos entre este servidor de destino y el servidor principal. Ésta es la configuración predeterminada. A menos que tenga una razón concreta para elegir un valor diferente, se recomienda no modificarlo.|  
  
Si se especifica **1** o **2** , debe tener habilitado SSL en los servidores maestro y de destino. Si se especifica **2** , debe tener además un certificado debidamente firmado presente en el servidor maestro.  
  
> [!CAUTION]  
> [!INCLUDE[ssNoteRegistry](../../includes/ssnoteregistry_md.md)]  
  
## <a name="see-also"></a>Vea también  
[Cómo habilitar conexiones cifradas en el motor de base de datos (Administrador de configuración de SQL Server)](http://msdn.microsoft.com/en-us/e1e55519-97ec-4404-81ef-881da3b42006)  
  

