---
title: MSSQLSERVER_15599 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 15599 (Database Engine error)
ms.assetid: 97e427a9-8587-46ea-954b-974b5df9c223
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c51b30e8af7c075c4b84ab04311aae5961919339
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47778033"
---
# <a name="mssqlserver15599"></a>MSSQLSERVER_15599
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|15599|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|SEC_LOCAL_TEMP_AUDIT_PERMISSIONS|  
|Texto del mensaje|No se pueden establecer permisos ni auditoría y en objetos temporales locales.|  
  
## <a name="explanation"></a>Explicación  
La auditoría y los permisos no tienen ningún efecto cuando se establecen en objetos locales o globales temporales. Las instrucciones no producen un error (las operaciones vuelven correctamente), pero no tienen ningún efecto.  
  
Este comportamiento no ha cambiado, pero a partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], este mensaje informativo alerta al usuario.  
  
## <a name="user-action"></a>Acción del usuario  
No es necesaria ninguna acción, pero considere la posibilidad de quitar las instrucciones que intentan establecer la auditoría o los permisos en objetos locales o globales temporales.  
  
