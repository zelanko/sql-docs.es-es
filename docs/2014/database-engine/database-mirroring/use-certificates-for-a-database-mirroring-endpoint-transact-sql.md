---
title: Usar certificados para un punto de conexión de creación de reflejo de la base de datos (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- database mirroring [SQL Server], deployment
- certificates [SQL Server], database mirroring
- authentication [SQL Server], database mirroring
- database mirroring [SQL Server], security
ms.assetid: f7c23cc2-48dc-4b78-b441-89ca29a0bd9e
caps.latest.revision: 32
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 1cd5203c202111272d2205c9e524e80b950dbed7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36196984"
---
# <a name="use-certificates-for-a-database-mirroring-endpoint-transact-sql"></a>Usar certificados para un extremo de creación de reflejo de la base de datos (Transact-SQL)
  Para habilitar la autenticación de certificados para la creación de reflejos de la base de datos en una instancia determinada del servidor, el administrador del sistema debe configurar cada instancia del servidor para que utilice certificados en las conexiones de entrada y salida. Las conexiones de salida deben configurarse en primer lugar.  
  
> [!NOTE]  
>  Todas las conexiones de creación de reflejo en una instancia de servidor utilizan un único extremo de reflejo de la base de datos; debe especificar el método de autenticación de la instancia de servidor cuando cree el extremo. Por tanto, en la creación de reflejo de la base de datos solo puede utilizar un formulario de autenticación por cada instancia de servidor.  
  
## <a name="configuring-outbound-connections"></a>Configurar conexiones salientes  
 Siga estos pasos en cada instancia de servidor que configure para la creación de reflejo de la base de datos:  
  
1.  En la base de datos **maestra** , cree una clave maestra de base de datos.  
  
2.  En la base de datos **maestra** , cree un certificado cifrado en la instancia de servidor.  
  
3.  Cree un extremo para la instancia de servidor utilizando su certificado.  
  
4.  Realice una copia de seguridad del certificado en un archivo. A continuación, cópiela de forma segura a los demás sistemas.  
  
 Debe completar estos pasos para cada asociado y el testigo, si existe.  
  
 Para obtener más información, vea [Permitir que un punto de conexión de creación de reflejo de la base de datos utilice certificados para las conexiones salientes &#40;Transact-SQL&#41;](database-mirroring-use-certificates-for-outbound-connections.md).  
  
## <a name="configuring-inbound-connections"></a>Configurar conexiones entrantes  
 A continuación, siga estos pasos para cada asociado que configure para la creación de reflejo de la base de datos. En la base de datos **maestra** :  
  
1.  Cree un inicio de sesión para el otro sistema.  
  
2.  Cree un usuario para dicho inicio de sesión.  
  
3.  Obtenga el certificado para el extremo de reflejo de la otra instancia de servidor.  
  
4.  Asociar el certificado al usuario creado en el paso 2.  
  
5.  Conceda el permiso CONNECT para el inicio de sesión para el extremo de reflejo.  
  
 Si existe un testigo, también debe configurar conexiones de entrada para él. Esto requiere la configuración de inicios de sesión, usuarios y certificados para el testigo en los dos asociados y viceversa.  
  
 Para obtener más información, vea [Permitir que un punto de conexión de creación de reflejo de la base de datos utilice certificados para las conexiones entrantes &#40;Transact-SQL&#41;](database-mirroring-use-certificates-for-inbound-connections.md).  
  
## <a name="security"></a>Seguridad  
 A menos que garantice que su red es segura, se recomienda utilizar el cifrado para las conexiones de creación de reflejo de la base de datos. Para obtener más información, vea [El punto de conexión de creación de reflejo de la base de datos &#40;SQL Server&#41;](the-database-mirroring-endpoint-sql-server.md).  
  
 Cuando copie un certificado en otro sistema, utilice un método de copia seguro. Tenga mucho cuidado de mantener todos sus certificados protegidos.  
  
## <a name="see-also"></a>Vea también  
 [Crear la clave maestra de una base de datos](../../relational-databases/security/encryption/create-a-database-master-key.md)   
 [CREATE MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-master-key-transact-sql)   
 [Seguridad de transporte para la creación de reflejo de base de datos y grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](transport-security-database-mirroring-always-on-availability.md)   
 [Centro de seguridad para el motor de base de datos SQL Server y la base de datos SQL Azure](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)   
 [El punto de conexión de creación de reflejo de la base de datos &#40;SQL Server&#41;](the-database-mirroring-endpoint-sql-server.md)  
  
  
