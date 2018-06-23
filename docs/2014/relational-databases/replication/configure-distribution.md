---
title: Configurar la distribución | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- replication [SQL Server], distribution
- distribution configuration [SQL Server replication]
- remote Distributors [SQL Server replication]
- transactional replication, configuring distribution
- distribution databases [SQL Server replication], sizing
- Distributors [SQL Server replication], configuring
- distribution databases [SQL Server replication], about distribution databases
- distribution databases [SQL Server replication]
- merge replication [SQL Server replication], configuring distribution
ms.assetid: 94d52169-384e-4885-84eb-2304e967d9f7
caps.latest.revision: 43
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: fdbb5ced844290625222036e0d670e93cbd08a77
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36202686"
---
# <a name="configure-distribution"></a>Configurar la distribución
  El distribuidor es un servidor que contiene la base de datos de distribución, que almacena metadatos y datos del historial de todos los tipos de replicación y transacciones para la replicación transaccional. Para configurar la replicación, debe configurar un distribuidor. Un publicador solamente se puede asignar a una instancia del distribuidor, aunque varios publicadores pueden compartir un distribuidor. El distribuidor utiliza estos recursos adicionales en el servidor en el que se encuentra:  
  
-   Espacio de disco adicional, si los archivos de instantáneas de la publicación se almacenan en el distribuidor (la situación habitual)  
  
-   Espacio de disco adicional para almacenar la base de datos de distribución.  
  
-   Uso adicional del procesador por los agentes de replicación para las suscripciones de inserción que se ejecutan en el distribuidor  
  
 El servidor seleccionado como distribuidor debe disponer del espacio en disco y la capacidad de proceso adecuados para la replicación y cualquier otra actividad asignada a ese servidor. Al configurar el distribuidor, debe especificar:  
  
-   Una carpeta de instantáneas que se utiliza, de manera predeterminada, para todos los publicadores que usen este distribuidor. Asegúrese de que la carpeta esté compartida y tenga establecidos los permisos adecuados. Para más información, vea [Proteger la carpeta de instantáneas](security/secure-the-snapshot-folder.md).  
  
-   El nombre y la ubicación de los archivos de la base de datos de distribución. No se puede cambiar el nombre de la base de datos de distribución una vez creada. Si desea utilizar un nombre distinto para la base de datos, debe deshabilitar la distribución y volver a configurar la base de datos.  
  
-   Todos los publicadores autorizados para utilizar el distribuidor. Si especifica otros publicadores además de la instancia en la que se ejecuta el distribuidor, debe especificar también una contraseña para las conexiones entre los publicadores y el distribuidor remoto.  
  
 Para la replicación transaccional después de configurar la distribución, se recomienda:  
  
-   Ajustar la base de datos de distribución a un tamaño apropiado. Pruebe la replicación con una carga típica para el sistema con el fin de determinar cuánto espacio se necesita para almacenar comandos. Asegúrese de que la base de datos es lo suficientemente grande para almacenar comandos sin recurrir al crecimiento automático con frecuencia. Para más información sobre cómo cambiar el tamaño de una base de datos, vea [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql).  
  
-   Configurar la opción **sync with backup** en la base de datos de distribución. Para más información, vea [Strategies for Backing Up and Restoring Snapshot and Transactional Replication](administration/strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication.md) (Estrategias para hacer copias de seguridad y restaurar replicación de instantáneas o replicación transaccional) y [Enable Coordinated Backups for Transactional Replication &#40;Replication Transact-SQL Programming&#41;](administration/enable-coordinated-backups-for-transactional-replication.md) (Habilitar copias de seguridad coordinadas para la replicación transaccional &#40;programación de la replicación con Transact-SQL&#41;).  
  
## <a name="local-and-remote-distributors"></a>Distribuidores locales y remotos  
 De forma predeterminada, el distribuidor es el mismo servidor que el publicador (un distribuidor local), aunque también puede ser un servidor distinto del publicador (un distribuidor remoto). Por lo general, se elige un distribuidor remoto cuando se desea:  
  
-   Descargar el proceso en otro equipo para que la replicación tenga un impacto mínimo en el publicador (por ejemplo, si el publicador es un servidor OLTP).  
  
-   Configurar un distribuidor centralizado para varios publicadores.  
  
 Los distribuidores remotos son más frecuentes en la replicación transaccional que en la replicación de mezcla por dos motivos:  
  
-   El distribuidor tiene un rol más amplio en la replicación transaccional porque todas las transacciones replicadas se escriben y se leen en la base de datos de distribución.  
  
-   Las topologías de replicación de mezcla usan por lo general suscripciones de extracción, de forma que los agentes se ejecutan en cada suscriptor en lugar de ejecutarse todos en el distribuidor. Para más información, vea [Subscribe to Publications](subscribe-to-publications.md) (Suscribirse a publicaciones). En la mayoría de los casos, debe usar un distribuidor local para la replicación de mezcla.  
  
 Para configurar la publicación y la distribución, vea [Configure Publishing and Distribution](configure-publishing-and-distribution.md).  
  
 Para modificar las propiedades del distribuidor y del publicador, vea [View and Modify Distributor and Publisher Properties](view-and-modify-distributor-and-publisher-properties.md).  
  
## <a name="see-also"></a>Vea también  
 [Publicar datos y objetos de base de datos](publish/publish-data-and-database-objects.md)   
 [Proteger el distribuidor](security/secure-the-distributor.md)  
  
  
