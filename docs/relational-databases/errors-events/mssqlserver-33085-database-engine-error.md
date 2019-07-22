---
title: MSSQLSERVER_33085 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 33085 (Database Engine error)
ms.assetid: c27b8d1d-668a-4ba8-8b61-25a5ebbc5485
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6eb560fb30d71ba16a153b3101c6f85a2194ca3c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67908445"
---
# <a name="mssqlserver33085"></a>MSSQLSERVER_33085
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|33085|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|SEC_CRYPTOPROVE_METHOD_CANNOT_FOUND|  
|Texto del mensaje|Uno o más métodos no se pueden encontrar en la biblioteca de proveedores de servicios criptográficos '%.*ls'.|  
  
## <a name="explanation"></a>Explicación  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no pudo utilizar el proveedor de servicios criptográficos enumerado en el mensaje de error. El proveedor de servicios criptográficos no admitió un método necesario. El estado del error indica qué método no se encontró.  
  
|State|Descripción|  
|---------|---------------|  
|1|SqlCryptInitializeProvider|  
|2|SqlCryptFreeProvider|  
|3|SqlCryptOpenSession|  
|4|SqlCryptCloseSession|  
|5|SqlCryptGetProviderInfo|  
|6|SqlCryptGetNextAlgorithmId|  
|7|SqlCryptGetAlgorithmInfo|  
|8|SqlCryptCreateKey|  
|9|SqlCryptDropKey|  
|10|SqlCryptGetNextKeyId|  
|11|SqlCryptGetKeyInfoByKeyId|  
|12|SqlCryptGetKeyInfoByThumb|  
|13|SqlCryptGetKeyInfoByName|  
|14|SqlCryptExportKey|  
|15|SqlCryptImportKey|  
|16|SqlCryptEncrypt|  
|17|SqlCryptDecrypt|  
  
## <a name="user-action"></a>Acción del usuario  
Póngase en contacto con el proveedor de servicios criptográficos para obtener más información.  
  
