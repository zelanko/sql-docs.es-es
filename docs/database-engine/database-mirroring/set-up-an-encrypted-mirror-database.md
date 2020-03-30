---
title: Establecer una base de datos reflejada cifrada| Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- cryptography [SQL Server], database mirroring
- encryption [SQL Server], database mirroring
- database master key [SQL Server], database mirroring
- mirror database [SQL Server]
- database mirroring [SQL Server], security
ms.assetid: 7329a575-be29-46e0-abc6-1344db37920c
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: e96342ca114ae06d2c1d75954ccd32a674f900a4
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "68025227"
---
# <a name="set-up-an-encrypted-mirror-database"></a>Establecer una base de datos reflejada cifrada
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Para habilitar el descifrado automático de la clave maestra de base de datos de una base de datos reflejada, debe proporcionar la contraseña que usó para cifrar la clave maestra a la instancia del servidor reflejado. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y las versiones posteriores incluyen mecanismos para transferir la contraseña. Use **sp_control_dbmasterkey_password** para crear una credencial para la clave maestra de base de datos antes de iniciar la creación de reflejo de la base de datos. Debe repetir este proceso para cada base de datos que se vaya a reflejar. Para obtener más información, vea [sp_control_dbmasterkey_password &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-control-dbmasterkey-password-transact-sql.md).  
  
> [!CAUTION]  
>  No habilite el descifrado por error de una base de datos que debe permanecer inaccesible a **sa** y a otras entidades de seguridad de servidor con amplios privilegios. Puede configurar una base de datos de forma que su jerarquía de claves no pueda descifrarse con la clave maestra de servicio. Esta opción se admite como una defensa a fondo para bases de datos que contienen información que no debe estar accesible para **sa** u otras entidades de seguridad de servidor con muchos privilegios. Si habilita el descifrado de conmutación por error de este tipo de bases de datos eliminará la defensa a fondo, permitiendo así que **sa** y otras entidades de seguridad de servidor con muchos privilegios descifren la base de datos.  
  
## <a name="see-also"></a>Consulte también  
 [sp_control_dbmasterkey_password &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-control-dbmasterkey-password-transact-sql.md)   
 [CREATE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md)   
 [ALTER MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-master-key-transact-sql.md)   
 [Jerarquía de cifrado](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [Configurar la creación de reflejo de la base de datos &#40;SQL Server&#41;](../../database-engine/database-mirroring/setting-up-database-mirroring-sql-server.md)  
  
  
