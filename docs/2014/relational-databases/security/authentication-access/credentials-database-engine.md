---
title: Credenciales (motor de base de datos) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-security
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- principals [SQL Server], credentials
- schemas [SQL Server], credentials
- permissions [SQL Server], credentials
- groups [SQL Server], credentials
- ALTER ANY CREDENTIAL permission
- security [SQL Server], credentials
- authentication [SQL Server], credentials
- users [SQL Server], credentials
- credentials [SQL Server], about credentials
- credentials [SQL Server]
ms.assetid: c8df6022-e0b4-46b8-9670-3f86938d3177
caps.latest.revision: 28
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 9de71af86c410658ab37aa1959ab2c9962b30a1c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36111981"
---
# <a name="credentials-database-engine"></a>Credenciales (motor de base de datos)
  Una credencial es un registro que contiene la información de autenticación (credenciales) necesaria para conectarse a un recurso situado fuera de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Esta información la utiliza [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]internamente. La mayoría de las credenciales incluyen un nombre de usuario y una contraseña de Windows.  
  
 La información almacenada en una credencial permite al usuario que se ha conectado a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mediante la autenticación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] obtener acceso a recursos situados fuera de la instancia del servidor. Cuando el recurso externo es Windows, el usuario se autentica como el usuario de Windows especificado en la credencial. Se puede asignar una única credencial a varios inicios de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Sin embargo, un inicio de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] solo se puede asignar a una credencial.  
  
 Las credenciales del sistema se crean de forma automática y se asocian a extremos específicos. Los nombres de las credenciales del sistema comienzan por dos signos de número (##).  
  
 Para obtener más información acerca de las credenciales, consulte el [sys.credentials](/sql/relational-databases/system-catalog-views/sys-credentials-transact-sql) vista de catálogo.  
  
## <a name="related-content"></a>Contenido relacionado  
 [Crear una credencial](../authentication-access/create-a-credential.md) [crear CREDENCIAL &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-credential-transact-sql)  
  
 [Proteger SQL Server](../securing-sql-server.md)  
  
  
