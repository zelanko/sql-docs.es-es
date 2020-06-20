---
title: MSSQLSERVER_33027 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 33027 (Database Engine error)
ms.assetid: bfdc626e-7958-4511-987d-3b687824e8af
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: f6bb461b42b66368224fffd2c14f9b4da61abf5b
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85033855"
---
# <a name="mssqlserver_33027"></a>MSSQLSERVER_33027
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|33027|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|SEC_CRYPTOPROV_CANTLOADDLL|  
|Texto del mensaje|No se pudo cargar el proveedor de servicios criptográficos '%.*ls' debido a una firma Authenticode o una ruta de archivo no válida. Revise los mensajes de otros errores anteriores.|  
  
## <a name="explanation"></a>Explicación  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no ha podido utilizar el proveedor de servicios criptográficos enumerado en el mensaje de error porque [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no ha podido cargar la DLL. O el nombre no es válido o la firma Authenticode no es válida.  
  
## <a name="user-action"></a>Acción del usuario  
 Compruebe que el archivo está presente y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tiene permiso de acceso a esa ubicación. Compruebe el registro de errores para ver posibles mensajes relacionados adicionales. De lo contrario, póngase en contacto con el proveedor de servicios criptográficos para obtener más información.  
  
  
