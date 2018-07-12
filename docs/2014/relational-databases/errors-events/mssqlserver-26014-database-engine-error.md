---
title: MSSQLSERVER_26014 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 26014 (Database Engine error)
ms.assetid: e2b0dfc7-0681-4e5d-8875-1d5f63534086
caps.latest.revision: 10
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b018c28ec8f718d74d00aec1cdb6fa74b9140118
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37411044"
---
# <a name="mssqlserver26014"></a>MSSQLSERVER_26014
    
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
  
  
