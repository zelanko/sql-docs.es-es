---
title: "Identidad y control de acceso (replicaci&#243;n) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "controles de acceso [replicación de SQL Server]"
  - "seguridad [replicación de SQL Server], identidad y control de acceso"
  - "autenticación [replicación de SQL Server]"
  - "identidad [replicación]"
ms.assetid: 4da0e793-1ee4-4f69-a80b-45c6732a238d
caps.latest.revision: 8
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 8
---
# Identidad y control de acceso (replicaci&#243;n)
  La autenticación es el proceso por el que una entidad (normalmente un equipo en este contexto) comprueba que otra entidad, también se denomina un *principal*, (normalmente otro equipo o usuario) es lo que dice ser. La autorización es el proceso por el que a una entidad de seguridad autenticada se le proporciona acceso a recursos, como a un archivo en el sistema de archivos o a una tabla en una base de datos.  
  
 La seguridad de replicación utiliza la autenticación y autorización para controlar el acceso a objetos de bases de datos replicadas y a los equipos y agentes que intervienen en el proceso de replicación. Esto se consigue con tres mecanismos:  
  
-   Seguridad del agente  
  
     El modelo de seguridad del agente de replicación permite un control perfecto de las cuentas con las que los agentes de replicación se ejecutan y realizan las conexiones. Para obtener más información sobre el modelo de seguridad del agente, vea [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md). Para obtener información acerca de inicios de sesión y contraseñas de agentes, consulte [administrar inicios de sesión y contraseñas en la replicación](../../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md).  
  
-   Roles de administración  
  
     Asegúrese de que se utilizan los roles de base de datos y servidor correctos en la configuración, mantenimiento y proceso de la replicación. Para más información, consulte [Security Role Requirements for Replication](../../../relational-databases/replication/security/security-role-requirements-for-replication.md).  
  
-   Lista de acceso a la publicación (PAL)  
  
     Conceda acceso a las publicaciones mediante la PAL. La PAL funciona de forma similar a las listas de control de acceso de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows. Cuando un suscriptor se conecta al publicador o al distribuidor y solicita acceso a una publicación, la información de autenticación transferida por el agente se comprueba con la PAL. Para obtener más información y prácticas recomendadas para la PAL, consulte [proteger el publicador](../../../relational-databases/replication/security/secure-the-publisher.md).  
  
## Filtrar datos publicados  
 Además de utilizar la autenticación y la autorización para controlar el acceso a objetos y datos replicados, la replicación incluye dos opciones para controlar qué datos están disponibles en un suscriptor: el filtro de columnas y el filtro de filas. Para obtener más información acerca del filtrado, consulte [filtrar datos publicados](../../../relational-databases/replication/publish/filter-published-data.md).  
  
 Cuando se define una restricción, se pueden publicar solo las columnas necesarias para la publicación y omitir las que no son necesarias o contienen datos confidenciales. Por ejemplo, al publicar la tabla **Customer** de la base de datos Adventure Works para representantes de ventas que están de viaje, puede omitir la columna **AnnualSales** , que solo sería importante para los ejecutivos de la compañía.  
  
 El filtrado de los datos publicados permite restringir el acceso a los datos y especificar qué datos están disponibles en el suscriptor. Por ejemplo, se puede filtrar la tabla **Customer** para que los socios corporativos solo reciban información de los clientes que en la columna **ShareInfo** tienen el valor "yes". Para la replicación de mezcla, existen consideraciones de seguridad que se deben tener en cuenta si utiliza un filtro con parámetros que incluya HOST_NAME(). Para obtener más información, vea la sección "Filtrar con HOST_NAME ()" en [filtros de fila parametrizados](../../../relational-databases/replication/merge/parameterized-row-filters.md).  
  
## Vea también  
 [Seguridad y protección & #40; Replicación y nº 41;](../../../relational-databases/replication/security/security-and-protection-replication.md)   
 [Información general sobre seguridad & #40; Replicación y nº 41;](../../../relational-databases/replication/security/security-overview-replication.md)   
 [Amenaza y mitigación de vulnerabilidades y Nº 40; Replicación y nº 41;](../../../relational-databases/replication/security/threat-and-vulnerability-mitigation-replication.md)  
  
  