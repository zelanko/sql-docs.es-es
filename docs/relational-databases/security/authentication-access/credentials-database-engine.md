---
title: Credenciales (motor de base de datos) | Microsoft Docs
ms.custom: 
ms.date: 02/27/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: "31"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.openlocfilehash: 42937069314e8f2c607871d950dce0fedb937e23
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="credentials-database-engine"></a>Credenciales (motor de base de datos)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../../includes/tsql-appliesto-ss2008-all-md.md)]

  Una credencial es un registro que contiene la información de autenticación (credenciales) necesaria para conectarse a un recurso situado fuera de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Esta información la utiliza [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]internamente. La mayoría de las credenciales incluyen un nombre de usuario y una contraseña de Windows.  
  
 La información almacenada en una credencial permite al usuario que se ha conectado a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mediante la autenticación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] obtener acceso a recursos situados fuera de la instancia del servidor. Cuando el recurso externo es Windows, el usuario se autentica como el usuario de Windows especificado en la credencial. Se puede asignar una única credencial a varios inicios de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Sin embargo, un inicio de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] solo se puede asignar a una credencial.  
  
 Para conocer las credenciales que se almacenan en la base de datos maestra y se pueden usar en la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], vea [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-credential-transact-sql.md). Para obtener más información sobre las credenciales usadas por una base de datos específica y portables con esa base de datos, vea [CREATE DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-database-scoped-credential-transact-sql.md).  
  
 Las credenciales del sistema se crean de forma automática y se asocian a extremos específicos. Los nombres de las credenciales del sistema comienzan por dos signos de número (##).  
  
 Para obtener más información sobre las credenciales, vea las vistas de catálogo [sys.credentials](../../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md) y [sys.database_scoped_credentials](../../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md).  
  
## <a name="related-content"></a>Contenido relacionado  
 [Crear una credencial](../../../relational-databases/security/authentication-access/create-a-credential.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-credential-transact-sql.md)   
 [CREATE DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-database-scoped-credential-transact-sql.md)  
 [Proteger SQL Server](../../../relational-databases/security/securing-sql-server.md)  
  
  
