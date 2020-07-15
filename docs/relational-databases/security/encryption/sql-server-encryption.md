---
title: Cifrado de SQL Server | Microsoft Docs
description: Use estos recursos para entender cómo emplea SQL Server el cifrado para mejorar la seguridad de las bases de datos.
ms.custom: ''
ms.date: 05/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- encryption [SQL Server], about encryption
- security [SQL Server], encryption
- cryptography [SQL Server], about cryptography
ms.assetid: ead0150e-4943-4ad5-84c8-36f85c7278f4
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d749c2707c78aa452bdb6a55f2f2d477ea0fb465
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85720431"
---
# <a name="sql-server-encryption"></a>Cifrado de SQL Server
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  El cifrado es el proceso consistente en ofuscar los datos mediante el uso de una clave o contraseña. Esto puede hacer que los datos sean inútiles sin la clave o contraseña de descifrado correspondiente. El cifrado no resuelve los problemas de control de acceso. Sin embargo, mejora la seguridad debido a que limita la pérdida de datos, incluso si se superan los controles de acceso. Por ejemplo, si el equipo host de base de datos no está configurado correctamente y un usuario malintencionado obtiene datos confidenciales, esa información robada podría resultar inservible si está cifrada.  
  

> [!IMPORTANT]  
>  Aunque el cifrado es una valiosa herramienta para ayudar a garantizar la seguridad, no está indicado para todos los datos o conexiones. Cuando decida si debe implementar el cifrado, debe tener en cuenta el modo en que los usuarios obtendrán acceso a los datos. Si los usuarios tienen acceso a los datos a través de una red pública, podría ser necesario el cifrado de datos para aumentar la seguridad. Sin embargo, si todo el acceso se realiza dentro de una configuración de intranet segura, el cifrado podría no ser necesario. Cualquier uso del cifrado también debería incluir una estrategia de mantenimiento para las contraseñas, las claves y los certificados.  
  
> [!NOTE]  
>  Encontrará la información más reciente sobre la seguridad de la capa de transporte (TLS1.2) en [Soporte de TLS 1.2 para Microsoft SQL Server](https://support.microsoft.com/kb/3135244).  

Puede utilizar el cifrado en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para las conexiones, los datos y los procedimientos almacenados. En la tabla siguiente, se incluye más información sobre el cifrado en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  

 [Jerarquía de cifrado](../../../relational-databases/security/encryption/encryption-hierarchy.md)  
 Información acerca de la jerarquía de cifrado de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 [Elegir un algoritmo de cifrado](../../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)  
 Información acerca del modo de seleccionar un algoritmo de cifrado efectivo.  
  
 [Cifrado de datos transparente &#40;TDE&#41;](../../../relational-databases/security/encryption/transparent-data-encryption.md)  
 Información general sobre cómo cifrar datos de forma transparente.  
  
 [SQL Server y claves de cifrado de base de datos &#40;motor de base de datos&#41;](../../../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md)  
 En [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], las claves de cifrado incluyen una combinación de claves públicas, privadas y simétricas que se utilizan para proteger la información confidencial. En esta sección se explica cómo implementar y administrar las claves de cifrado.  
  
 [Always Encrypted &#40;motor de base de datos&#41;](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)  
 Asegurarse de que los administradores de base de datos local, los operadores de base de datos en la nube u otros usuarios con privilegios elevados, pero no autorizados, no puedan obtener acceso a los datos cifrados.  
  
 [Enmascaramiento de datos dinámicos](../../../relational-databases/security/dynamic-data-masking.md)  
 Limitar la exposición de información confidencial ocultándola a los usuarios sin privilegios.  
  
 [Certificados y claves asimétricas de SQL Server](../../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md)  
 Información sobre el uso de criptografía de clave pública.  
  
## <a name="related-content"></a>Contenido relacionado  
 [Proteger SQL Server](../../../relational-databases/security/securing-sql-server.md)  
 Información general sobre el modo de proteger la plataforma [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y cómo trabajar con los usuarios y los objetos protegibles.  

[Información general sobre las funcionalidades de seguridad de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-security-overview)
</br>Información general de seguridad de Azure SQL Database para proteger los datos, controlar el acceso y la supervisión proactiva.
  
 [Funciones de cifrado &#40;Transact-SQL&#41;](../../../t-sql/functions/cryptographic-functions-transact-sql.md)  
 Información sobre el modo de implementar las funciones criptográficas.  
  
 [ENCRYPTBYPASSPHRASE &#40;Transact-SQL&#41;](../../../t-sql/functions/encryptbypassphrase-transact-sql.md)  
 Información sobre cómo utilizar una contraseña para cifrar datos.  
  
 [ENCRYPTBYKEY &#40;Transact-SQL&#41;](../../../t-sql/functions/encryptbykey-transact-sql.md)  
 Información sobre cómo utilizar una clave simétrica para cifrar datos.  
  
 [ENCRYPTBYASYMKEY &#40;Transact-SQL&#41;](../../../t-sql/functions/encryptbyasymkey-transact-sql.md)  
 Información sobre cómo utilizar una clave asimétrica para cifrar datos.  
  
 [ENCRYPTBYCERT &#40;Transact-SQL&#41;](../../../t-sql/functions/encryptbycert-transact-sql.md)  
 Información sobre cómo utilizar un certificado para cifrar datos.  
  
## <a name="external-resources"></a>Recursos externos  
 [Microsoft TechNet: SQL Server TechCenter: Seguridad y protección de SQL Server 2012](https://download.microsoft.com/download/8/F/A/8FABACD7-803E-40FC-ADF8-355E7D218F4C/SQL_Server_2012_Security_Best_Practice_Whitepaper_Apr2012.docx)  
 Información actual sobre la seguridad en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="see-also"></a>Consulte también  
 [sys.key_encryptions &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-key-encryptions-transact-sql.md)   
 [SQL Server y claves de cifrado de base de datos &#40;motor de base de datos&#41;](../../../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md)   
 [Hacer copia de seguridad y restaurar claves de cifrado de Reporting Services](../../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)     
 [Habilitación de conexiones cifradas en el motor de base de datos](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)    
  
  
