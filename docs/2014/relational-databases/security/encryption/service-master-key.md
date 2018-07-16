---
title: Clave maestra de servicio | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- service master key [SQL Server]
- service master key [SQL Server], about service master key
ms.assetid: 85f2095d-2590-4f59-8a29-7e100edd02bb
caps.latest.revision: 17
author: aliceku
ms.author: aliceku
manager: craigg
ms.openlocfilehash: bf45a708f34ed5a22e733287e3ec240817e91a9b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37286991"
---
# <a name="service-master-key"></a>clave maestra de servicio
  La clave maestra de servicio es la raíz de la jerarquía de cifrado de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Se genera automáticamente la primera vez que se necesita para cifrar otra clave. De manera predeterminada, la clave maestra de servicio se cifra mediante la API de protección de datos de Windows y utilizando la clave del equipo local. La clave maestra de servicio solo puede abrirla la cuenta de servicio de Windows bajo la que se creó, o una entidad de seguridad con acceso al nombre y a la contraseña de la cuenta de servicio.  
  
 Para regenerar o restaurar la clave maestra de servicio, es necesario descifrar y volver a cifrar toda la jerarquía de cifrado. A no ser que se haya vulnerado la seguridad de la clave, esta operación que hace un uso intensivo de los recursos se debe programar durante un período de poca actividad.  
  
 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usa el algoritmo de cifrado AES para proteger la clave maestra de servicio (SMK) y la clave maestra de la base de datos (DMK). AES es un algoritmo de cifrado más reciente que el algoritmo 3DES empleado en versiones anteriores. Después de actualizar una instancia de [!INCLUDE[ssDE](../../../includes/ssde-md.md)] a [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], se deben volver a generar las claves SMK y DMK para actualizar las claves maestras al algoritmo AES. Para obtener más información sobre cómo volver a generar la SMK, vea [ALTER SERVICE MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-service-master-key-transact-sql) y [ALTER MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-master-key-transact-sql).  
  
## <a name="best-practice"></a>Práctica recomendada  
 Cree una copia de seguridad de la clave maestra de servicio y almacene esta copia en una ubicación segura fuera del sitio.  
  
## <a name="related-tasks"></a>Related Tasks  
 [BACKUP SERVICE MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-service-master-key-transact-sql)  
  
 [RESTORE SERVICE MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-service-master-key-transact-sql)  
  
 [ALTER SERVICE MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-service-master-key-transact-sql)  
  
## <a name="see-also"></a>Vea también  
 [Jerarquía de cifrado](encryption-hierarchy.md)  
  
  
