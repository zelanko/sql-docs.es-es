---
description: Identidad y Access Control (replicación)
title: Identidad y control de acceso (replicación) | Microsoft Docs
ms.custom: ''
ms.date: 11/20/2018
ms.prod: sql
ms.prod_service: database-engine
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
monikerRange: =azuresqldb-mi-current||>=sql-server-2016
ms.openlocfilehash: 8737fa7c4781110c4a9169a7334e88f7df734291
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97479766"
---
# <a name="identity-and-access-control-replication"></a>Identidad y Access Control (replicación)
[!INCLUDE[sql-asdbmi](../../../includes/applies-to-version/sql-asdbmi.md)]
  La autenticación es el proceso por el que una entidad (normalmente un equipo en este contexto) comprueba que otra entidad, denominada *principal*(normalmente otro equipo o usuario) es quien o lo que dice ser. La autorización es el proceso por el que a una entidad de seguridad autenticada se le proporciona acceso a recursos, como a un archivo en el sistema de archivos o a una tabla en una base de datos.  
  
 La seguridad de replicación utiliza la autenticación y autorización para controlar el acceso a objetos de bases de datos replicadas y a los equipos y agentes que intervienen en el proceso de replicación. Esto se consigue con tres mecanismos:  
  
-   Seguridad del agente  
  
     El modelo de seguridad del agente de replicación permite un control perfecto de las cuentas con las que los agentes de replicación se ejecutan y realizan las conexiones. Para obtener más información sobre el modelo de seguridad del agente, vea [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md). 
  
-   Roles de administración  
  
     Asegúrese de que se utilizan los roles de base de datos y servidor correctos en la configuración, mantenimiento y proceso de la replicación. Para más información, consulte [Security Role Requirements for Replication](../../../relational-databases/replication/security/security-role-requirements-for-replication.md).  
  
-   Lista de acceso a la publicación (PAL)  
  
     Conceda acceso a las publicaciones mediante la PAL. La PAL funciona de forma similar a las listas de control de acceso de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows. Cuando un suscriptor se conecta al publicador o al distribuidor y solicita acceso a una publicación, la información de autenticación transferida por el agente se comprueba con la PAL. Para más información y prácticas recomendadas para la PAL, vea [Secure the Publisher](../../../relational-databases/replication/security/secure-the-publisher.md) (Proteger el publicador).  
  
## <a name="filtering-published-data"></a>Filtrar datos publicados  
 Además de utilizar la autenticación y la autorización para controlar el acceso a objetos y datos replicados, la replicación incluye dos opciones para controlar qué datos están disponibles en un suscriptor: el filtro de columnas y el filtro de filas. Para más información sobre el filtrado, vea [Filtrar datos publicados](../../../relational-databases/replication/publish/filter-published-data.md).  
  
 Cuando se define una restricción, se pueden publicar solo las columnas necesarias para la publicación y omitir las que no son necesarias o contienen datos confidenciales. Por ejemplo, al publicar la tabla **Customer** de la base de datos Adventure Works para representantes de ventas que están de viaje, puede omitir la columna **AnnualSales** , que solo sería importante para los ejecutivos de la compañía.  
  
 El filtrado de los datos publicados permite restringir el acceso a los datos y especificar qué datos están disponibles en el suscriptor. Por ejemplo, se puede filtrar la tabla **Customer** para que los socios corporativos solo reciban información de los clientes que en la columna **ShareInfo** tienen el valor "yes". Para la replicación de mezcla, existen consideraciones de seguridad que se deben tener en cuenta si utiliza un filtro con parámetros que incluya HOST_NAME(). Para obtener más información, vea la sección "Filtrar con HOST_NAME()" en [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  

## <a name="manage-logins-and-passwords-in-replication"></a>Administrar inicios de sesión y contraseñas en la replicación
Cuando configure la replicación, especifique los inicios de sesión y las contraseñas para los agentes de replicación. Después de configurar la replicación, puede cambiar los inicios de sesión y las contraseñas. Para más información, consulte [View and Modify Replication Security Settings](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md). Si cambia la contraseña de una cuenta usada por un agente de replicación, ejecute [sp_changereplicationserverpasswords &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changereplicationserverpasswords-transact-sql.md).  

La compatibilidad con el uso de cuentas de servicio administradas de grupo (gMSA) se introdujo en SQL Server 2014. Para más información, vea el blog de [Replicación y cuentas de servicio administradas de grupo](https://repltalk.com/2019/03/26/replication-and-group-managed-service-accounts/).
  
## <a name="see-also"></a>Consulte también  
 [Mitigar amenazas y vulnerabilidades &#40;replicación&#41;](../../../relational-databases/replication/security/threat-and-vulnerability-mitigation-replication.md) [Modelo de seguridad del Agente de replicación](../../../relational-databases/replication/security/replication-agent-security-model.md)   
 [Procedimientos recomendados de seguridad de replicación](../../../relational-databases/replication/security/replication-security-best-practices.md)   

  
  
