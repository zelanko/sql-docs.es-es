---
title: Contraseñas seguras | Microsoft Docs
description: Obtenga información sobre las contraseñas en SQL Server y descubra qué constituye una contraseña segura para mejorar la seguridad de su implementación.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- logins [SQL Server], passwords
- passwords [SQL Server], strong
- symbols [SQL Server]
- security [SQL Server], passwords
- passwords [SQL Server], symbols
- characters [SQL Server], password policies
- strong passwords [SQL Server]
ms.assetid: 338548f4-c4d8-47ca-b597-5c9c0f2fa205
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ac636ae2b994b359921e164fe884de80a7d3486a
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/06/2020
ms.locfileid: "86001043"
---
# <a name="strong-passwords"></a>Contraseñas seguras
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
  Las contraseñas pueden constituir el vínculo más débil de una implementación de seguridad de servidor. Tenga cuidado a la hora de seleccionar una contraseña. Una contraseña segura presenta las siguientes características:  
  
-   Tiene ocho caracteres como mínimo.  
  
-   Contiene una combinación de letras, números y símbolos.  
  
-   No es una palabra que pueda encontrarse en el diccionario.  
  
-   No es el nombre de un comando.  
  
-   No es el nombre de una persona.  
  
-   No es el nombre de un usuario.  
  
-   No es el nombre de un equipo.  
  
-   Se cambia con frecuencia.  
  
-   Presenta diferencias con respecto a contraseñas anteriores.  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pueden contener hasta 128 caracteres, entre los que se pueden incluir letras, símbolos y dígitos. Dado que los inicios de sesión, nombres de usuario, roles y contraseñas se utilizan con frecuencia en instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] , determinados símbolos deberán estar incluidos entre comillas dobles (") o corchetes ([ ]). Utilice estos delimitadores en las instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] cuando el inicio de sesión, usuario, rol o contraseña de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] presente las siguientes características:  
  
-   Contiene o comienza por un carácter de espacio.  
  
-   Comienza por el carácter $ o \@.  
  
 Si se usa en una cadena de conexión OLE DB u ODBC, un inicio de sesión o una contraseña no deben contener ninguno de estos caracteres: [] () , ; ? * ! \@ =. Estos caracteres se usan para inicializar una conexión o para separar valores de conexión.  
  
## <a name="related-content"></a>Contenido relacionado  
 [Directiva de contraseñas](../../relational-databases/security/password-policy.md)  
  
  
