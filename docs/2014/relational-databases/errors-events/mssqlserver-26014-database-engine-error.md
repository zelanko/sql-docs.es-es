---
title: MSSQLSERVER_26014 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 26014 (Database Engine error)
ms.assetid: e2b0dfc7-0681-4e5d-8875-1d5f63534086
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: edebfb36a1693f2a7d6a94d7c006d80e2bb27683
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62914628"
---
# <a name="mssqlserver_26014"></a>MSSQLSERVER_26014
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|26014|  
|Origen de eventos|MSSQLSERVER|  
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
  
  
