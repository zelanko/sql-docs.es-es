---
title: Credenciales (motor de base de datos) | Microsoft Docs
description: Obtenga información sobre las credenciales en SQL Server. Familiarícese con la información de autenticación necesaria para conectarse a un recurso fuera de SQL Server.
ms.custom: ''
ms.date: 06/27/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8f6be70be8c7f2d03c55c5df53fd9f27a32b35fa
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/06/2020
ms.locfileid: "86005662"
---
# <a name="credentials-database-engine"></a>Credenciales (motor de base de datos)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Una credencial es un registro que contiene la información de autenticación (credenciales) necesaria para conectarse a un recurso situado fuera de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Esta información la utiliza [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]internamente. La mayoría de las credenciales incluyen un nombre de usuario y una contraseña de Windows.  
  
 La información almacenada en una credencial permite al usuario que se ha conectado a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mediante la autenticación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] obtener acceso a recursos situados fuera de la instancia del servidor. Cuando el recurso externo es Windows, el usuario se autentica como el usuario de Windows especificado en la credencial. Una credencial solo puede asignarse a un único inicio de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Y un inicio de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] solo puede asignarse a una credencial.  
  
 Para conocer las credenciales que se almacenan en la base de datos maestra y se pueden usar en la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], vea [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-credential-transact-sql.md). Para obtener más información sobre las credenciales usadas por una base de datos específica y portables con esa base de datos, vea [CREATE DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-database-scoped-credential-transact-sql.md).  
  
 Las credenciales del sistema se crean de forma automática y se asocian a extremos específicos. Los nombres de las credenciales del sistema comienzan por dos signos de número (##).  
  
 Para obtener más información sobre las credenciales, vea las vistas de catálogo [sys.credentials](../../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md) y [sys.database_scoped_credentials](../../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md).  
  
## <a name="related-content"></a>Contenido relacionado  
 [Crear una credencial](../../../relational-databases/security/authentication-access/create-a-credential.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-credential-transact-sql.md)   
 [CREATE DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-database-scoped-credential-transact-sql.md)  
 [Proteger SQL Server](../../../relational-databases/security/securing-sql-server.md)  
  
  
