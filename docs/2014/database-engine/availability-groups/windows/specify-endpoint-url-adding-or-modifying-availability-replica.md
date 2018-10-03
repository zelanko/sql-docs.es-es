---
title: Especifique la dirección URL del extremo al agregar o modificar una réplica de disponibilidad (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- endpoints [SQL Server], AlwaysOn Availability Groups
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], endpoint
- Endpoint URLs (HADR)
ms.assetid: d7520c13-a8ee-4ddc-9e9a-54cd3d27ef1c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 94cf3cff73e98718db6e097f13dcab47cd676ed4
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48097187"
---
# <a name="specify-the-endpoint-url-when-adding-or-modifying-an-availability-replica-sql-server"></a>Especificar la dirección URL del extremo al agregar o modificar una réplica de disponibilidad (SQL Server)
  Para hospedar una réplica de disponibilidad de un grupo de disponibilidad, una instancia de servidor debe poseer un extremo de creación de reflejo de la base de datos. La instancia de servidor utiliza este extremo para escuchar los mensajes de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] procedentes de las réplicas de disponibilidad hospedadas por otras instancias del servidor. Para definir una réplica de disponibilidad para un grupo de disponibilidad, debe especificar la dirección URL del extremo de la instancia del servidor que hospedará la réplica. La *dirección URL del extremo* identifica el protocolo de transporte del extremo de creación de reflejo de la base de datos—TCP, la dirección del sistema de la instancia del servidor y el número de puerto asociado con el extremo.  
  
> [!NOTE]  
>  El término “dirección URL del extremo” es sinónimo del término “dirección de red del servidor” que usa la interfaz de usuario y la documentación de creación de reflejo de la base de datos.  
  
-   [Sintaxis de una dirección URL del extremo](#SyntaxOfURL)  
  
-   [Buscar el nombre de dominio completo de un sistema](#Finding_FQDN)  
  
-   [Tareas relacionadas](#RelatedTasks)  
  
-   [Contenido relacionado](#RelatedContent)  
  
##  <a name="SyntaxOfURL"></a> Sintaxis de una dirección URL del extremo  
 La sintaxis de una dirección URL del extremo tiene el siguiente formato:  
  
 TCP**://***\<system-address>***:***\<port>*  
  
 donde  
  
-   *\<dirección del sistema>* es una cadena que identifica de forma inequívoca el equipo de destino. Generalmente, la dirección del servidor es un nombre del sistema (si los sistemas están en el mismo dominio), un nombre de dominio completo o una dirección IP:  
  
    -   Dado que todos los nodos del clúster de conmutación por error de Windows Server (WSFC) están en el mismo dominio, puede usar el nombre del equipo; por ejemplo, `SYSTEM46`.  
  
    -   Para utilizar una dirección IP, ésta debe ser única en el entorno. Recomendamos que utilice una dirección IP solo si es estática. La dirección IP puede ser IP Versión 4 (IPv4) o IP Versión 6 (IPv6). Las direcciones IPv6 se deben incluir entre corchetes, por ejemplo: **[***<dirección_IPv6>***]**.  
  
         Para conocer la dirección IP de un sistema, en el símbolo del sistema de Windows, escriba el comando **ipconfig** .  
  
    -   El nombre de dominio completo siempre funciona. Esta es una cadena de dirección definida localmente que adopta diferentes formatos en distintos lugares. Con frecuencia, aunque no siempre, el nombre de dominio completo es un nombre compuesto que incluye el nombre del equipo y una serie de segmentos de dominio separados por puntos con el siguiente formato:  
  
         *nombre_equipo* **.** *segmento_de_dominio*[...**.***segmento_de_dominio*]  
  
         donde *nombre_de_equipo*es el nombre de red del equipo que ejecuta la instancia de servidor y *segmento_de_dominio*[...**.***segmento_de_dominio*] es la información restante de dominio del servidor; por ejemplo: `localinfo.corp.Adventure-Works.com`.  
  
         El contenido y el número de segmentos de dominio se determinan en la empresa u organización. Para obtener más información, vea [Buscar el nombre de dominio completo](#Finding_FQDN), más adelante en este tema.  
  
-   *\<puerto>* es el número de puerto usado por el punto de conexión de reflejo de la instancia del servidor asociado.  
  
     Un extremo de creación de reflejo de la base de datos puede utilizar cualquier puerto disponible en el equipo. Cada número de puerto debe estar asociado con un único extremo y cada extremo está asociado con una sola instancia de servidor; en consecuencia, diferentes instancias del mismo servidor escuchan en diferentes extremos con distintos puertos. Por consiguiente, el puerto que especifique en la dirección URL del extremo al especificar una réplica de disponibilidad siempre dirigirá los mensajes entrantes a la instancia de servidor cuyo extremo esté asociado con dicho puerto.  
  
     En la dirección URL del extremo, solo el número de puerto identifica la instancia del servidor que está asociada con el extremo de creación de reflejo en el equipo de destino. En la siguiente ilustración se muestran las direcciones de extremo de dos instancias de servidor en un solo equipo. La instancia predeterminada usa el puerto `7022` y la instancia con nombre usa el puerto `7033`. Las direcciones URL del extremo para estas dos instancias de servidor son, respectivamente, `TCP://MYSYSTEM.Adventure-works.MyDomain.com:7022` y `TCP://MYSYSTEM.Adventure-works.MyDomain.com:7033`. Observe que la dirección no contiene el nombre de la instancia de servidor.  
  
     ![Direcciones de red del servidor de una instancia predeterminada](../../media/dbm-2-instances-ports-1-system.gif "Direcciones de red del servidor de una instancia predeterminada")  
  
     Para identificar el puerto asociado actualmente al extremo de creación de reflejo de la base de datos de una instancia de servidor, utilice la siguiente instrucción [!INCLUDE[tsql](../../../includes/tsql-md.md)] :  
  
    ```  
    SELECT type_desc, port FROM sys.TCP_endpoints  
    ```  
  
     Busque la fila cuyo valor **type_desc** sea "DATABASE_MIRRORING" y use el número de puerto correspondiente.  
  
### <a name="examples"></a>Ejemplos  
  
#### <a name="a-using-a-system-name"></a>A. Usar un nombre de sistema  
 La siguiente dirección URL del extremo especifica un nombre de sistema, `SYSTEM46`, y el puerto `7022`.  
  
 `TCP://SYSTEM46:7022`  
  
#### <a name="b-using-a-fully-qualified-domain-name"></a>B. Usar un nombre de dominio completo  
 La siguiente dirección URL del extremo especifica un nombre de dominio completo, `DBSERVER8.manufacturing.Adventure-Works.com`, y el puerto `7024`.  
  
 `TCP://DBSERVER8.manufacturing.Adventure-Works.com:7024`  
  
#### <a name="c-using-ipv4"></a>C. Usar IPv4  
 La siguiente dirección URL del extremo especifica una dirección IPv4, `10.193.9.134`, y el puerto `7023`.  
  
 `TCP://10.193.9.134:7023`  
  
#### <a name="d-using-ipv6"></a>D. Usar IPv6  
 La siguiente dirección URL del extremo contiene una dirección IPv6, `2001:4898:23:1002:20f:1fff:feff:b3a3`, y el puerto `7022`.  
  
 `TCP://[2001:4898:23:1002:20f:1fff:feff:b3a3]:7022`  
  
##  <a name="Finding_FQDN"></a> Buscar el nombre de dominio completo de un sistema  
 Para buscar el nombre de dominio completo de un sistema, en el símbolo del sistema de Windows de ese sistema, escriba:  
  
 **IPCONFIG /ALL**  
  
 Para formar el nombre de dominio completo, concatene los valores de *<host_name>* y *<Primary_Dns_Suffix>* de la siguiente manera:  
  
 *&lt;nombre_host&gt;* **.** *<sufijo_DNS_primario>*  
  
 Por ejemplo, la configuración IP  
  
 `Host Name  .  .  .  .  .  .  : MYSERVER`  
  
 `Primary Dns Suffix  .  .  .  : mydomain.Adventure-Works.com`  
  
 equivale al siguiente nombre de dominio completo:  
  
 `MYSERVER.mydomain.Adventure-Works.com`  
  
> [!NOTE]  
>  Si necesita más información acerca de un nombre de dominio completo, póngase en contacto con el administrador del sistema.  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
 **Para configurar un extremo de creación del reflejo de la base de datos**  
  
-   [Crear una base de datos de extremo de reflejo para grupos de disponibilidad AlwaysOn &#40;PowerShell de SQL Server&#41;](database-mirroring-always-on-availability-groups-powershell.md)  
  
-   [Crear un punto de conexión de creación de reflejo de la base de datos para la autenticación de Windows &#40;Transact-SQL&#41;](../../database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)  
  
-   [Usar certificados para un punto de conexión de creación de reflejo de la base de datos &#40;Transact-SQL&#41;](../../database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)  
  
    -   [Permitir que un punto de conexión de creación de reflejo de la base de datos utilice certificados para las conexiones salientes &#40;Transact-SQL&#41;](../../database-mirroring/database-mirroring-use-certificates-for-outbound-connections.md)  
  
    -   [Permitir que un punto de conexión de creación de reflejo de la base de datos use certificados para las conexiones entrantes &#40;Transact-SQL&#41;](../../database-mirroring/database-mirroring-use-certificates-for-inbound-connections.md)  
  
-   [Especificar una dirección de red de servidor &#40;creación de reflejo de la base de datos&#41;](../../database-mirroring/specify-a-server-network-address-database-mirroring.md)  
  
-   [Solución de problemas de configuración de grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;eliminado](troubleshoot-always-on-availability-groups-configuration-sql-server.md)  
  
 **Para ver información acerca del extremo de creación de reflejo de la base de datos**  
  
-   [sys.database_mirroring_endpoints &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql)  
  
 **Para agregar una réplica de disponibilidad**  
  
-   [Agregar una réplica secundaria a un grupo de disponibilidad &#40;SQL Server&#41;](add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [Combinar una réplica secundaria con un grupo de disponibilidad &#40;SQL Server&#41;](join-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
##  <a name="RelatedContent"></a> Contenido relacionado  
  
-   [Guía de soluciones de Microsoft SQL Server AlwaysOn para alta disponibilidad y recuperación ante desastres](http://go.microsoft.com/fwlink/?LinkId=227600)  
  
## <a name="see-also"></a>Vea también  
 [Creación y configuración de grupos de disponibilidad &#40;SQL Server&#41;](creation-and-configuration-of-availability-groups-sql-server.md)   
 [Información general de grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [CREATE ENDPOINT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-endpoint-transact-sql)  
  
  
