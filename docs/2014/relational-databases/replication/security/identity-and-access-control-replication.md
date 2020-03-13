---
title: Identidad y control de acceso (replicación) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- access controls [SQL Server replication]
- security [SQL Server replication], identity and access control
- authentication [SQL Server replication]
- identity [Replication]
ms.assetid: 4da0e793-1ee4-4f69-a80b-45c6732a238d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: cd51a3e4c139c52d6510140324ae042c653377b5
ms.sourcegitcommit: 4baa8d3c13dd290068885aea914845ede58aa840
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/13/2020
ms.locfileid: "79289523"
---
# <a name="identity-and-access-control-replication"></a>Identidad y Access Control (replicación)
  La autenticación es el proceso por el que una entidad (normalmente un equipo en este contexto) comprueba que otra entidad, denominada *principal*(normalmente otro equipo o usuario) es quien o lo que dice ser. La autorización es el proceso por el que a una entidad de seguridad autenticada se le proporciona acceso a recursos, como a un archivo en el sistema de archivos o a una tabla en una base de datos.  
  
 La seguridad de replicación utiliza la autenticación y autorización para controlar el acceso a objetos de bases de datos replicadas y a los equipos y agentes que intervienen en el proceso de replicación. Esto se consigue con tres mecanismos:  
  
-   Seguridad del agente: el modelo de seguridad del agente de replicación permite un control exhaustivo sobre las cuentas en las que los agentes de replicación se ejecutan y realizan conexiones. Para obtener más información sobre el modelo de seguridad del agente, vea [Replication Agent Security Model](replication-agent-security-model.md). Para información sobre inicios de sesión y contraseñas para agentes, vea [Manage Logins and Passwords in Replication](identity-and-access-control-replication.md#manage-logins-and-passwords-in-replication) (Administrar inicios de sesión y contraseñas en la replicación).  
  
-   Roles de administración: Asegúrese de que se usan los roles de servidor y de base de datos correctos para la configuración de la replicación, el mantenimiento y el procesamiento. Para más información, consulte [Security Role Requirements for Replication](security-role-requirements-for-replication.md).  
  
-   La lista de acceso a la publicación (PAL): concede acceso a las publicaciones a través de la PAL. La PAL funciona de forma similar a las listas de control de acceso de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows. Cuando un suscriptor se conecta al publicador o al distribuidor y solicita acceso a una publicación, la información de autenticación transferida por el agente se comprueba con la PAL. Para más información y prácticas recomendadas para la PAL, vea [Secure the Publisher](secure-the-publisher.md) (Proteger el publicador).  
  
## <a name="filtering-published-data"></a>Filtrar datos publicados  
 Además de utilizar la autenticación y la autorización para controlar el acceso a objetos y datos replicados, la replicación incluye dos opciones para controlar qué datos están disponibles en un suscriptor: el filtro de columnas y el filtro de filas. Para más información sobre el filtrado, vea [Filtrar datos publicados](../publish/filter-published-data.md).  
  
 Cuando se define una restricción, se pueden publicar solo las columnas necesarias para la publicación y omitir las que no son necesarias o contienen datos confidenciales. Por ejemplo, al publicar la tabla **Customer** de la base de datos Adventure Works para representantes de ventas que están de viaje, puede omitir la columna **AnnualSales** , que solo sería importante para los ejecutivos de la compañía.  
  
 El filtrado de los datos publicados permite restringir el acceso a los datos y especificar qué datos están disponibles en el suscriptor. Por ejemplo, se puede filtrar la tabla **Customer** para que los socios corporativos solo reciban información de los clientes que en la columna **ShareInfo** tienen el valor "yes". Para la replicación de mezcla, existen consideraciones de seguridad que se deben tener en cuenta si utiliza un filtro con parámetros que incluya HOST_NAME(). Para obtener más información, vea la sección "Filtrar con HOST_NAME()" en [Parameterized Row Filters](../merge/parameterized-filters-parameterized-row-filters.md).  

## <a name="manage-logins-and-passwords-in-replication"></a>Administrar inicios de sesión y contraseñas en la replicación
  Cuando configure la replicación, especifique los inicios de sesión y las contraseñas para los agentes de replicación. Después de configurar la replicación, puede cambiar los inicios de sesión y las contraseñas. Para obtener más información, vea [ver y modificar la configuración de seguridad](view-and-modify-replication-security-settings.md)de la replicación. Si cambia la contraseña de una cuenta usada por un agente de replicación, ejecute [sp_changereplicationserverpasswords &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changereplicationserverpasswords-transact-sql).  
  
## <a name="see-also"></a>Consulte también  
 [Modelo de seguridad del Agente de replicación](replication-agent-security-model.md)   
 [Replication Security Best Practices](replication-security-best-practices.md)   
 [Seguridad de Replicación de SQL Server](view-and-modify-replication-security-settings.md)   
 [Amenaza de replicación y mitigación de vulnerabilidades](threat-and-vulnerability-mitigation-replication.md)   

  
  
