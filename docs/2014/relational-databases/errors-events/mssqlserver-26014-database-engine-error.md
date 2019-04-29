---
title: MSSQLSERVER_26014 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 26014 (Database Engine error)
ms.assetid: e2b0dfc7-0681-4e5d-8875-1d5f63534086
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: edebfb36a1693f2a7d6a94d7c006d80e2bb27683
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62914628"
---
# <a name="mssqlserver26014"></a>MSSQLSERVER_26014
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|26014|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|SNI_SSL_USER_CERT_FAILURE|  
|Texto del mensaje|No se puede cargar el certificado especificado por el usuario [Cert Hash (sha1) "%hs"]. El servidor no acepta una conexión. Debe comprobar que el certificado está correctamente instalado. Consulte el tema sobre cómo configurar un certificado para usarlo con SSL en los Libros en pantalla.|  
  
## <a name="explanation"></a>Explicación  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] trató de cargar el certificado mencionado en el mensaje pero se produjo un error en la operación. Se debe resolver este problema para que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pueda utilizar este certificado.  
  
Entre las posibles causas del error figuran:  
  
-   El certificado puede haber sido movido o eliminado.  
  
-   Si el inicio de sesión usado por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ha cambiado, puede que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no disponga de permiso para tener acceso al certificado.  
  
-   El certificado puede haber expirado.  
  
## <a name="user-action"></a>Acción del usuario  
Asegúrese de que el certificado mencionado en el mensaje existe en el sistema, es accesible y es válido para utilizarse.  
  
