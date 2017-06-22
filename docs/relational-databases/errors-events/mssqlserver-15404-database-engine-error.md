---
title: MSSQLSERVER_15404 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 15404 (Database Engine error)
ms.assetid: 69677f02-bc81-4e4a-99b8-5c1bd1de36df
caps.latest.revision: 5
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 52499bb75078863b631912935b4ffbbd616c9aae
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver15404"></a>MSSQLSERVER_15404
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|15404|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|SEC_NTGRP_ERROR|  
|Texto del mensaje|No se pudo obtener información sobre el grupo o usuario de Windows NT '*user*', código de error *code*.|  
  
## <a name="explanation"></a>Explicación  
Se usa 15404 en la autenticación cuando se especifica una entidad de seguridad no válida. O bien, la suplantación de una cuenta de Windows genera errores porque no hay ninguna relación de plena confianza entre la cuenta de servicio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y el dominio de la cuenta de Windows.  
  
## <a name="user-action"></a>Acción del usuario  
Compruebe que la entidad de seguridad de Windows existe y está escrita correctamente.  
  
Si este error se debe a que no hay una relación de plena confianza entre la cuenta de servicio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y el dominio de la cuenta de Windows, una de las acciones siguientes puede resolver el error:  
  
-   Use una cuenta del mismo dominio que el usuario de Windows para el servicio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Si [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] emplea una cuenta de equipo como Network Service o Local System, el dominio que contiene el usuario de Windows debe confiar en el equipo.  
  
-   Use una cuenta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  

