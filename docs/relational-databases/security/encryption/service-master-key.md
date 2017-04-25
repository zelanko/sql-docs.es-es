---
title: Clave maestra de servicio | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- service master key [SQL Server]
- service master key [SQL Server], about service master key
ms.assetid: 85f2095d-2590-4f59-8a29-7e100edd02bb
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: fd1adfac8a64c19577374d309390bead0cb12de9
ms.lasthandoff: 04/11/2017

---
# <a name="service-master-key"></a>Clave maestra de servicio
  La clave maestra de servicio es la raíz de la jerarquía de cifrado de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Se genera automáticamente la primera vez que se necesita para cifrar otra clave. De manera predeterminada, la clave maestra de servicio se cifra mediante la API de protección de datos de Windows y utilizando la clave del equipo local. La clave maestra de servicio solo puede abrirla la cuenta de servicio de Windows bajo la que se creó, o una entidad de seguridad con acceso al nombre y a la contraseña de la cuenta de servicio.  
  
 Para regenerar o restaurar la clave maestra de servicio, es necesario descifrar y volver a cifrar toda la jerarquía de cifrado. A no ser que se haya vulnerado la seguridad de la clave, esta operación que hace un uso intensivo de los recursos se debe programar durante un período de poca actividad.  
  
 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usa el algoritmo de cifrado AES para proteger la clave maestra de servicio (SMK) y la clave maestra de la base de datos (DMK). AES es un algoritmo de cifrado más reciente que el algoritmo 3DES empleado en versiones anteriores. Después de actualizar una instancia de [!INCLUDE[ssDE](../../../includes/ssde-md.md)] a [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], se deben volver a generar las claves SMK y DMK para actualizar las claves maestras al algoritmo AES. Para obtener más información sobre cómo volver a generar la SMK, vea [ALTER SERVICE MASTER KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-service-master-key-transact-sql.md) y [ALTER MASTER KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-master-key-transact-sql.md).  
  
## <a name="best-practice"></a>Práctica recomendada  
 Cree una copia de seguridad de la clave maestra de servicio y almacene esta copia en una ubicación segura fuera del sitio.  
  
## <a name="related-tasks"></a>Tareas relacionadas  
 [BACKUP SERVICE MASTER KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/backup-service-master-key-transact-sql.md)  
  
 [RESTORE SERVICE MASTER KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/restore-service-master-key-transact-sql.md)  
  
 [ALTER SERVICE MASTER KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-service-master-key-transact-sql.md)  
  
## <a name="see-also"></a>Vea también  
 [Jerarquía de cifrado](../../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
