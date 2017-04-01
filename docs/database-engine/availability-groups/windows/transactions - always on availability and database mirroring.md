---
title: "Transacciones entre bases de datos y transacciones distribuidas para la creaci&#243;n de reflejo de la base de datos o grupos de disponibilidad AlwaysOn (SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "creación de reflejo de la base de datos [SQL Server], interoperabilidad"
  - "transacciones entre bases de datos [SQL Server]"
  - "transacciones [creación de reflejo de la base de datos]"
  - "Grupos de disponibilidad [SQL Server], interoperabilidad"
  - "solución de problemas [SQL Server], transacciones entre bases de datos"
ms.assetid: 9f7ed895-ad65-43e3-ba08-00d7bff1456d
caps.latest.revision: 33
ms.author: "mikeray"
manager: "jhubbard"
---
# Transacciones entre bases de datos y transacciones distribuidas para la creaci&#243;n de reflejo de la base de datos o grupos de disponibilidad AlwaysOn (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

En este tema se describe la compatibilidad de las transacciones entre bases de datos y distribuidas para la creación de reflejo de la base de datos y grupos de disponibilidad AlwaysOn.  
  
## Compatibilidad con transacciones entre bases de datos en la misma instancia de SQL Server  
Las transacciones entre bases de datos en la misma instancia de SQL Server no son compatibles para los grupos de disponibilidad AlwaysOn. Esto significa que la misma instancia de SQL Server no puede hospedar dos bases de datos en una transacción entre bases de datos. Esto ocurre incluso si esas bases de datos forman parte del mismo grupo de disponibilidad.  
  
Las transacciones entre bases de datos tampoco se admiten para la creación de reflejo de la base de datos.  
  
##  <a name="dtcsupport"></a> Compatibilidad con transacciones distribuidas  
Las transacciones distribuidas son compatibles con los grupos de disponibilidad AlwaysOn. Esto se aplica a las transacciones distribuidas entre bases de datos hospedadas en dos instancias diferentes de SQL Server. También se aplica a las transacciones distribuidas entre SQL Server y otro servidor compatible con DTC.  
 
Coordinador de transacciones distribuidas de Microsoft (MSDTC o DTC) es un servicio de Windows que proporciona infraestructura de transacciones para sistemas distribuidos. MSDTC permite que las aplicaciones cliente incluyan varios orígenes de datos en una transacción que luego se confirma en todos los servidores incluidos en la transacción. Por ejemplo, puede usar MSDTC para coordinar transacciones que abarcan varias bases de datos en servidores diferentes.

SQL Server 2016 ofrece la posibilidad de usar transacciones distribuidas en las que una o varias de las bases de datos de la transacción se encuentran en un grupo de disponibilidad. Antes de SQL Server 2016, no se admitían las transacciones distribuidas para bases de datos de grupos de disponibilidad. SQL Server 2016 puede registrar un administrador de recursos por base de datos. Esta nueva funcionalidad es la razón por la que las transacciones distribuidas pueden incluir bases de datos de grupos de disponibilidad.

  
 Se deben cumplir los requisitos siguientes:  
  
-   Los grupos de disponibilidad deben ejecutarse en Windows Server 2016 o Windows Server 2012 R2. Para Windows Server 2012 R2, debe instalar la actualización de KB3090973 disponible en [https://support.microsoft.com/es-es/kb/3090973](https://support.microsoft.com/en-us/kb/3090973).  
  
-   Los grupos de disponibilidad deben crearse con el comando **CREATE AVAILABILITY GROUP** y la cláusula **WITH DTC_SUPPORT = PER_DB**. Actualmente no se puede modificar un grupo de disponibilidad existente.  

- Todas las instancias de SQL Server que participarán en el grupo de disponibilidad deben ser de SQL Server 2016 o posterior.
  
 
 ## Sin compatibilidad con las transacciones distribuidas
 Los casos concretos en que no se admiten transacciones distribuidas incluyen:
 
 -  Si hay más de una base de datos implicada en la transacción en el mismo grupo de disponibilidad.
 
 -  Si al menos una base de datos se encuentra en un grupo de disponibilidad y otra base de datos se encuentra en la misma instancia de SQL Server. 
 
 -  Si el grupo de disponibilidad no se ha creado con la transacción distribuida habilitada.
 
 -  Creación de reflejo de base de datos.
 
 ## Recomendación
 En entornos de producción debería agrupar el servicio MSDTC. Si no agrupa el servicio DTC, SQL Server usará el servicio DTC local. Con el servicio DTC local, se reduce la disponibilidad general de la solución. Cuando DTC está agrupado, se pueden recuperar las transacciones en proceso si se produce un error en el nodo de clúster.
 
 > [!IMPORTANT]
 > Determine la salida predeterminada apropiada de las transacciones que DTC no puede resolver para el entorno.  Para información sobre cómo configurar la salida predeterminada, consulte [in-doubt xact resolution (opción de configuración del servidor)](../../../database-engine/configure-windows/in-doubt-xact-resolution-server-configuration-option.md).
  
## Escenario de ejemplo con la creación de reflejo de base de datos  
 En el siguiente ejemplo de creación de reflejo de la base de datos se muestra cómo podría producirse una incoherencia lógica. En este ejemplo, una aplicación utiliza una transacción entre bases de datos para insertar dos filas de datos: una fila se inserta en una tabla de una base de datos reflejada, A, y la otra fila se inserta en una tabla de otra base de datos, B. La base de datos A se está reflejando en modo de alta seguridad con conmutación automática por error. Mientras la transacción se confirma, la base de datos A deja de estar disponible y la sesión de creación de reflejo se conmuta por error automáticamente al reflejo de la base de datos A.  
  
 Después de la conmutación por error, la transacción entre bases de datos podría confirmarse correctamente en la base de datos B, pero no en la base de datos conmutada por error. Esto se produciría si el servidor principal original de la base de datos A no hubiese enviado el registro de transacciones entre bases de datos al servidor reflejado antes del error. Después de la conmutación por error, esa transacción no existiría en el nuevo servidor principal. Las bases de datos A y B se volverían incoherentes porque los datos insertados en la base de datos B se mantienen intactos, pero los datos insertados en la base de datos A se pierden.  
  
 Su puede producir un escenario similar cuando se usa una transacción de MS DTC. Por ejemplo, después de la conmutación por error, el nuevo servidor principal contacta con MS DTC. Sin embargo, MS DTC.no tiene conocimiento del nuevo servidor principal y termina las transacciones que están "preparadas para confirmar" y que otras bases de datos consideran confirmadas.  
  
> [!NOTE]  
>  No se permite usar la creación de reflejo de la base de datos con DTC ni usar los grupos de disponibilidad AlwaysOn con DTC de formas no aprobadas en este tema.  Esto no implica que los aspectos del producto no relacionados con DTC sean incompatibles; no obstante, no se admitirán los problemas derivados del uso incorrecto de las transacciones distribuidas.  
  
## Vea también  
 [Grupos de disponibilidad AlwaysOn: interoperabilidad &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-availability-groups-interoperability-sql-server.md)  
  
  