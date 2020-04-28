---
title: sp_changedistributor_password (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changedistributor_password
- sp_changedistributor_password_TSQL
helpviewer_keywords:
- sp_changedistributor_password
ms.assetid: 4a496e60-414a-4026-ba7a-3e89391d39b7
author: stevestein
ms.author: sstein
ms.openlocfilehash: 3715bfacd1a94f588992d7e6832814f50c076d1c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68768900"
---
# <a name="sp_changedistributor_password-transact-sql"></a>sp_changedistributor_password (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Cambia la contraseña de un distribuidor. Este procedimiento almacenado se ejecuta en el distribuidor de cualquier base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_changedistributor_password [ @password= ] 'password'   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @password = ] 'password'`Es la nueva contraseña. *password* es de **tipo sysname**y no tiene ningún valor predeterminado. Si el distribuidor es local, se cambia la contraseña del inicio de sesión del sistema **distributor_admin** .  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Observaciones  
 **sp_changedistributor_password** se utiliza en todos los tipos de replicación.  
  
## <a name="example"></a>Ejemplo  
 [!code-sql[HowTo#sp_changedistributor_password](../../relational-databases/replication/codesnippet/tsql/sp-changedistributor-pas_1.sql)]  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de servidor **sysadmin** pueden ejecutar **sp_changedistributor_password**.  
  
## <a name="see-also"></a>Consulte también  
 [Ver y modificar la configuración de seguridad de la replicación](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [Proteger el distribuidor](../../relational-databases/replication/security/secure-the-distributor.md)   
 [sp_adddistributor &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-adddistributor-transact-sql.md)   
 [Procedimientos almacenados de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
