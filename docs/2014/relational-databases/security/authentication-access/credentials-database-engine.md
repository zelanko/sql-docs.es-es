---
title: Credenciales (motor de base de datos) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
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
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: faa2b5be7cf6918b5d5232763a96ed4dbbc89e51
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85055360"
---
# <a name="credentials-database-engine"></a>Credenciales (motor de base de datos)
  Una credencial es un registro que contiene la información de autenticación (credenciales) necesaria para conectarse a un recurso situado fuera de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Esta información la utiliza [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]internamente. La mayoría de las credenciales incluyen un nombre de usuario y una contraseña de Windows.  
  
 La información almacenada en una credencial permite al usuario que se ha conectado a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mediante la autenticación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] obtener acceso a recursos situados fuera de la instancia del servidor. Cuando el recurso externo es Windows, el usuario se autentica como el usuario de Windows especificado en la credencial. Se puede asignar una única credencial a varios inicios de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Sin embargo, un inicio de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] solo se puede asignar a una credencial.  
  
 Las credenciales del sistema se crean de forma automática y se asocian a extremos específicos. Los nombres de las credenciales del sistema comienzan por dos signos de número (##).  
  
 Para obtener más información sobre las credenciales, vea la vista de catálogo [Sys. Credentials](/sql/relational-databases/system-catalog-views/sys-credentials-transact-sql) .  
  
## <a name="related-content"></a>Contenido relacionado  
 [Crear una](../authentication-access/create-a-credential.md) credencial de creación de credenciales [&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-credential-transact-sql)  
  
 [Proteger SQL Server](../securing-sql-server.md)  
  
  
