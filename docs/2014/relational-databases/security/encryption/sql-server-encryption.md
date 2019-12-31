---
title: Cifrado de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- encryption [SQL Server], about encryption
- security [SQL Server], encryption
- cryptography [SQL Server], about cryptography
ms.assetid: ead0150e-4943-4ad5-84c8-36f85c7278f4
author: jaszymas
ms.author: jaszymas
manager: craigg
ms.openlocfilehash: f2aa6c25f8e8741308ff8f8b5df93cb2af67ad91
ms.sourcegitcommit: 39ea690996a7390e3d13d6fb8f39d8641cd5f710
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/10/2019
ms.locfileid: "74957101"
---
# <a name="sql-server-encryption"></a>Cifrado de SQL Server
  El cifrado es el proceso consistente en ofuscar los datos mediante el uso de una clave o contraseña. Esto puede hacer que los datos sean inútiles sin la clave o contraseña de descifrado correspondiente. El cifrado no resuelve los problemas de control de acceso. Sin embargo, mejora la seguridad debido a que limita la pérdida de datos, incluso si se superan los controles de acceso. Por ejemplo, si el equipo host de base de datos no está configurado correctamente y un usuario malintencionado obtiene datos confidenciales, esa información robada podría resultar inservible si está cifrada.  
  
 Puede utilizar el cifrado en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para las conexiones, los datos y los procedimientos almacenados. La tabla siguiente contiene más información acerca del cifrado en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  Aunque el cifrado es una valiosa herramienta para ayudar a garantizar la seguridad, no está indicado para todos los datos o conexiones. Cuando decida si debe implementar el cifrado, debe tener en cuenta el modo en que los usuarios obtendrán acceso a los datos. Si los usuarios tienen acceso a los datos a través de una red pública, podría ser necesario el cifrado de datos para aumentar la seguridad. Sin embargo, si todo el acceso se realiza dentro de una configuración de intranet segura, el cifrado podría no ser necesario. Cualquier uso del cifrado también debería incluir una estrategia de mantenimiento para las contraseñas, las claves y los certificados.  
  
## <a name="in-this-section"></a>En esta sección  
 [Jerarquía de cifrado](encryption-hierarchy.md)  
 Información acerca de la jerarquía de cifrado de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 [Elegir un algoritmo de cifrado](choose-an-encryption-algorithm.md)  
 Información acerca del modo de seleccionar un algoritmo de cifrado efectivo.  
  
 [Cifrado de datos transparente &#40;TDE&#41;](transparent-data-encryption.md)  
 Información general sobre cómo cifrar datos de forma transparente.  
  
 [SQL Server y claves de cifrado de base de datos &#40;Motor de base de datos&#41;](sql-server-and-database-encryption-keys-database-engine.md)  
 En [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], las claves de cifrado incluyen una combinación de claves públicas, privadas y simétricas que se utilizan para proteger la información confidencial. En esta sección se explica cómo implementar y administrar las claves de cifrado.  
  
## <a name="related-content"></a>Contenido relacionado  
 [Protección de SQL Server](../securing-sql-server.md)  
 Información general sobre el modo de proteger la plataforma [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y cómo trabajar con los usuarios y los objetos protegibles.  
  
 [Funciones criptográficas &#40;Transact-SQL&#41;](/sql/t-sql/functions/cryptographic-functions-transact-sql)  
 Información sobre el modo de implementar las funciones criptográficas.  
  
 [ENCRYPTBYPASSPHRASE &#40;Transact-SQL&#41;](/sql/t-sql/functions/encryptbypassphrase-transact-sql)  
 Información sobre cómo utilizar una contraseña para cifrar datos.  
  
 [ENCRYPTBYKEY &#40;Transact-SQL&#41;](/sql/t-sql/functions/encryptbykey-transact-sql)  
 Información sobre cómo utilizar una clave simétrica para cifrar datos.  
  
 [ENCRYPTBYASYMKEY &#40;Transact-SQL&#41;](/sql/t-sql/functions/encryptbyasymkey-transact-sql)  
 Información sobre cómo utilizar una clave asimétrica para cifrar datos.  
  
 [ENCRYPTBYCERT, &#40;Transact-SQL&#41;](/sql/t-sql/functions/encryptbycert-transact-sql)  
 Información sobre cómo utilizar un certificado para cifrar datos.  
  
## <a name="external-resources"></a>Recursos externos  
 [10 pasos para SQL Server la seguridad 2005](https://www.itprotoday.com/sql-server/10-steps-sql-server-2005-security)  
 Información actual sobre la seguridad en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="see-also"></a>Véase también  
 [Sys. key_encryptions &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-key-encryptions-transact-sql)   
 [SQL Server y claves de cifrado de base de datos &#40;Motor de base de datos&#41;](sql-server-and-database-encryption-keys-database-engine.md)   
 [Copia de seguridad y restauración de claves de cifrado de Reporting Services](../../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)  
  
  
