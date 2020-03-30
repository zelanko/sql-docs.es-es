---
title: Creación de reflejos de base de datos en SQL Server
description: Describe la funcionalidad de creación de reflejo de la base de datos.
ms.date: 09/30/2019
dev_langs:
- csharp
ms.assetid: 89befaff-bb46-4290-8382-e67cdb0e3de9
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: c7ace2feb39bcc3f5f257c0ac2c7360649cfc33c
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "78896997"
---
# <a name="database-mirroring-in-sql-server"></a>Creación de reflejos de base de datos en SQL Server

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

La creación de reflejo de la base de datos de SQL Server permite mantener una copia, o reflejo, de una base de datos de SQL Server en un servidor en espera. La creación de reflejo garantiza que existan dos copias independientes de los datos en todo momento, lo que proporciona una alta disponibilidad y una redundancia completa de los datos. El proveedor de SqlClient de Microsoft para SQL Server ofrece compatibilidad implícita con la creación de reflejo de la base de datos, de modo que el desarrollador no tiene que realizar ninguna acción ni escribir ningún código una vez que se ha configurado para una base de datos de SQL Server. Además, el objeto <xref:Microsoft.Data.SqlClient.SqlConnection> admite un modo de conexión explícita que permite proporcionar el nombre de un servidor asociado de conmutación por error en <xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionString%2A>.  
  
La siguiente secuencia simplificada de eventos se produce para un objeto <xref:Microsoft.Data.SqlClient.SqlConnection> que tiene como destino una base de datos configurada para la creación de reflejo:  
  
1. La aplicación cliente se conecta correctamente a la base de datos principal y el servidor devuelve el nombre del servidor asociado, que se almacena en caché en el cliente.  
  
2. Si se produce un error en el servidor que contiene la base de datos principal o se interrumpe la conectividad, se pierde el estado de la transacción y la conexión. La aplicación cliente intenta volver a establecer una conexión con la base de datos principal y produce un error.  
  
3. A continuación, la aplicación cliente intenta establecer una conexión a la base de datos reflejada en el servidor asociado de forma transparente. Si se realiza correctamente, la conexión se redirige a la base de datos reflejada, que luego se convierte en la nueva base de datos principal.  
  
## <a name="specifying-the-failover-partner-in-the-connection-string"></a>Especificación del asociado de conmutación por error en la cadena de conexión  
Si proporciona el nombre de un servidor asociado de conmutación por error en la cadena de conexión, el cliente intentará establecer de forma transparente una conexión con el asociado de conmutación por error si la base de datos principal no está disponible cuando la aplicación cliente se conecta por primera vez.  
  
```csharp
";Failover Partner=PartnerServerName"  
```  
  
Si omite el nombre del servidor asociado de conmutación por error y la base de datos principal no está disponible cuando la aplicación cliente se conecta por primera vez, se genera una excepción <xref:Microsoft.Data.SqlClient.SqlException>.  
  
Cuando se abre una conexión <xref:Microsoft.Data.SqlClient.SqlConnection> correctamente, el servidor devuelve el nombre del asociado de conmutación por error y reemplaza los valores proporcionados en la cadena de conexión.  
  
> [!NOTE]
>  Debe especificar explícitamente el nombre del catálogo o la base de datos inicial en la cadena de conexión en los escenarios de creación de reflejo de la base de datos. Si el cliente recibe información de conmutación por error sobre una conexión para la que no se ha especificado de forma explícita un catálogo o una base de datos inicial, dicha información no se almacena en caché y la aplicación no intenta conmutar por error si el servidor principal da error. Si una cadena de conexión tiene un valor para el asociado de conmutación por error, pero no para el catálogo o la base de datos inicial, se genera una excepción `InvalidArgumentException`.  
  
## <a name="retrieving-the-current-server-name"></a>Recuperación del nombre del servidor actual  
En el caso de una conmutación por error, puede recuperar el nombre del servidor al que está conectada realmente la conexión actual mediante la propiedad <xref:Microsoft.Data.SqlClient.SqlConnection.DataSource%2A> de un objeto <xref:Microsoft.Data.SqlClient.SqlConnection>. El siguiente fragmento de código recupera el nombre del servidor activo, dando por sentado que la variable de conexión hace referencia a una conexión <xref:Microsoft.Data.SqlClient.SqlConnection>abierta.  
  
Cuando se produce un evento de conmutación por error y la conexión cambia al servidor reflejado, la propiedad **DataSource** se actualiza para reflejar el nombre del reflejo.  
  
```csharp  
string activeServer = connection.DataSource;  
```  
  
## <a name="sqlclient-mirroring-behavior"></a>Comportamiento de creación de reflejo de SqlClient  
El cliente siempre intenta conectarse al servidor principal actual. Si se produce un error, lo intenta al asociado de conmutación por error. Si la base de datos reflejada ya se ha cambiado al rol principal en el servidor asociado, la conexión se realiza correctamente y la nueva asignación de reflejo principal se envía al cliente y se almacena en caché durante la llamada a <xref:System.AppDomain>. No se almacena de forma permanente y no está disponible para las posteriores conexiones en un **AppDomain** o proceso diferente. Pero está disponible para las posteriores conexiones en el mismo **AppDomain**. Tenga en cuenta que otro **AppDomain** o proceso que se ejecute en el mismo equipo o en otro tiene siempre su grupo de conexiones que no se restablecen. En ese caso, si la base de datos principal se interrumpe, cada proceso o **AppDomain** da error una vez y el grupo se borra automáticamente.  
  
> [!NOTE]
>  La compatibilidad con la creación de reflejo en el servidor se configura por base de datos. Si las operaciones de manipulación de datos se ejecutan en otras bases de datos no incluidas en el conjunto principal o de reflejos, ya sea mediante nombres de varias partes o cambiando la base de datos actual, los cambios en estas otras bases de datos no se propagan en caso de error. No se genera ningún error cuando se modifican datos en una base de datos que no está reflejada. El desarrollador debe evaluar el posible impacto de esas operaciones.  
  
## <a name="next-steps"></a>Pasos siguientes
### <a name="database-mirroring-resources"></a>Recursos de creación de reflejo de la base de datos  
Para obtener documentación conceptual e información sobre la configuración, la implementación y la administración de la creación de reflejo, vea los siguientes recursos en la documentación de SQL Server.  
  
|Resource|Descripción|  
|--------------|-----------------|  
|[Creación de reflejo de la base de datos](../../../database-engine/database-mirroring/database-mirroring-sql-server.md)|Describe cómo establecer y configurar la creación de reflejo en SQL Server.|  
