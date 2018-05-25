---
title: Grupos de disponibilidad AlwaysOn para SQL Server en Linux | Documentos de Microsoft
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 11/27/2017
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: e37742d4-541c-4d43-9ec7-a5f9b2c0e5d1
ms.openlocfilehash: 7de4097fdc843097cbd2865e4a4f3986c392ac04
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2018
---
# <a name="always-on-availability-groups-on-linux"></a>Grupos de disponibilidad AlwaysOn en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artículo describen las características de grupos de disponibilidad AlwaysOn (AG) en Linux-based [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] las instalaciones. También se tratan las diferencias entre Linux - y clúster de conmutación por error de Windows Server (WSFC)-según grupos de disponibilidad. Consulte la [documentación basada en Windows](../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md) para los aspectos básicos de grupos de disponibilidad, como funcionan igual en Windows y Linux excepto el WSFC.

Desde la perspectiva de alto nivel, grupos de disponibilidad bajo [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] en Linux son los mismos que en las implementaciones basadas en WSFC. Esto significa que todas las limitaciones y características son los mismos, con algunas excepciones. Las principales diferencias son:

-   Coordinador de transacciones distribuidas de Microsoft (DTC) no es compatible con Linux en [!INCLUDE[sssql17-md](../includes/sssql17-md.md)]. Si las aplicaciones requieren el uso de transacciones distribuidas y necesitan un AG, implementar [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] en Windows.
-   Las implementaciones basadas en Linux use marcapasos en lugar de un WSFC.
-   A diferencia de la mayoría de las configuraciones de grupos de disponibilidad en Windows excepto el escenario de clúster del grupo de trabajo, marcapasos nunca requiere servicios de dominio de Active Directory (AD DS).
-   Cómo se producirá un error en un AG de un nodo a otro es diferente entre Windows y Linux.
-   Ciertas opciones de configuración como `required_synchronized_secondaries_to_commit` solo puede cambiarse mediante marcapasos en Linux, mientras que una instalación basada en WSFC utiliza Transact-SQL.

## <a name="number-of-replicas-and-cluster-nodes"></a>Número de réplicas y los nodos del clúster

Un AG en [!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)] puede tener dos réplicas total: uno principal y otra secundaria solo pueden usarse para fines de disponibilidad. No puede utilizarse para todo lo demás, como las consultas legibles. Un AG en [!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)] puede tener hasta nueve réplicas total: uno principal y hasta ocho réplicas secundarias, de los cuales hasta tres (incluido el principal) puede ser sincrónica. Si utiliza un clúster subyacente, puede haber un máximo de 16 nodos total cuando está implicada Corosync. Un grupo de disponibilidad puede abarcar a lo sumo nueve de los 16 nodos con [!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)]y dos con [!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)].

Una configuración de dos réplicas que requiere la capacidad de conmutar por error automáticamente a otra réplica requiere el uso de una réplica de solo configuración, como se describe en [solo configuración de réplica y quórum](#configuration-only-replica-and-quorum). Réplicas de solo configuración se introdujeron en [!INCLUDE[sssql17-md](../includes/sssql17-md.md)] actualización acumulativa 1 (CU1), por lo que debe ser la versión mínima implementada para esta configuración.

Si se usan marcapasos, se debe configurar correctamente para que permanezca activados y ejecutándose. Esto significa que el quórum y STONITH deben implementarse correctamente desde la perspectiva marcapasos, además de cualquier [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] requisitos como una réplica de configuración.

Réplicas secundarias legibles solo son compatibles con [!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)].

## <a name="cluster-type-and-failover-mode"></a>Modo de conmutación por error y el tipo de clúster

Nuevo para [!INCLUDE[sssql17-md](../includes/sssql17-md.md)] es la introducción de un tipo de clúster para grupos de disponibilidad. Para Linux, hay dos valores válidos: externos y ninguno. Un tipo de clúster de externo significa que se utilizará marcapasos debajo de disponibilidad. Uso externo para tipo de clúster requiere que el modo de conmutación por error se establece en externa también (también es nuevo en [!INCLUDE[sssql17-md](../includes/sssql17-md.md)]). Se admite la conmutación automática por error, pero a diferencia de un WSFC, el modo de conmutación por error se establece en externa, no automático, cuando se usan marcapasos. A diferencia de un WSFC, se crea la parte marcapasos de disponibilidad después de configura el AG.

Un tipo de clúster de None significa que no hay ningún requisito para ni el AG utilizará, marcapasos. Incluso en servidores que tengan marcapasos configurado, si es un AG configurado con un tipo de clúster de None, marcapasos no detectará ni administrar ese AG. Un tipo de clúster de None solo admite failover manual de un servidor principal a una réplica secundaria. Un AG creado con ninguna se destinan principalmente para la lectura escalada del escenario, así como las actualizaciones. Aunque puede trabajar en escenarios como la recuperación ante desastres o disponibilidad local cuando no sea necesario conmutación automática por error, no se recomienda. También es más complejo sin marcapasos el caso del agente de escucha.

Tipo de clúster se almacena en la [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] vista de administración dinámica (DMV) `sys.availability_groups`, en las columnas `cluster_type` y `cluster_type_desc`.

## <a name="requiredsynchronizedsecondariestocommit"></a>requiere\_sincronizado\_secundarias\_a\_confirmación

Nuevo a [!INCLUDE[sssql17-md](../includes/sssql17-md.md)] es un valor que se usa por grupos de disponibilidad denominados `required_synchronized_secondaries_to_commit`. Esto indica la AG el número de réplicas secundarias que deben estar en forma sincronizada con la principal. Esto permite cosas como conmutación automática por error (solo cuando se integra con marcapasos con un tipo de clúster de externo) y controla el comportamiento de elementos como la disponibilidad de la réplica principal si el número correcto de las réplicas secundarias es en línea o sin conexión. Para comprender mejor cómo funciona esto, consulte [alta disponibilidad y protección de datos para las configuraciones de grupo de disponibilidad](sql-server-linux-availability-group-ha.md). El `required_synchronized_secondaries_to_commit` valor se establece de forma predeterminada y se mantiene por marcapasos /[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]. Puede invalidar este valor manualmente.

La combinación de `required_synchronized_secondaries_to_commit` y el nuevo número de secuencia (que se almacena en `sys.availability_groups`) informa marcapasos y [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] que, por ejemplo, puede suceder conmutación automática por error. En ese caso, una réplica secundaria tendría el mismo número de secuencia que la réplica principal, lo que significa que está actualizado con toda la información de configuración más reciente.

Hay tres valores que se pueden establecer para `required_synchronized_secondaries_to_commit`: 0, 1 o 2. Controlan el comportamiento de lo que sucede cuando una réplica deja de estar disponible. Los números corresponden al número de réplicas secundarias que deben sincronizarse con el servidor principal. El comportamiento es como se indica a continuación en Linux:

-   0: conmutación automática por error no es posible porque no hay ninguna réplica secundaria se necesita sincronizar. La base de datos principal está disponible en todo momento.
-   1: una réplica secundaria debe estar en un estado sincronizado con la principal; es posible que la conmutación automática por error. La base de datos principal no está disponible hasta que una réplica secundaria sincrónica está disponible.
-   2 – ambas réplicas secundarias en una configuración de AG de tres o más nodos deben estar sincronizadas con el elemento principal; es posible que la conmutación automática por error.

`required_synchronized_secondaries_to_commit` controla no solo el comportamiento de las conmutaciones por error con réplicas sincrónicas, pero la pérdida de datos. Con un valor de 1 o 2, una réplica secundaria es obligatorio que se sincronizarán, por tanto, siempre habrá redundancia de datos. Esto no significa que se pierdan datos.

Para cambiar el valor de `required_synchronized_secondaries_to_commit`, use la siguiente sintaxis:

>[!NOTE]
>Cambiar el valor hace que el recurso que se reinicie, lo que significa una breve interrupción. La única manera de evitarlo es establecer el recurso no estén administrados por el clúster temporalmente.

**Red Hat Enterprise Linux (RHEL) y Ubuntu**

```bash
sudo pcs resource update <AGResourceName> required_synchronized_secondaries_to_commit=<Value>
```

**SUSE Linux Enterprise Server (SLES)**

```bash
sudo crm resource param ms-<AGResourceName> set required_synchronized_secondaries_to_commit <value>
```

donde *AGResourceName* es el nombre del recurso configurado para el AG, y *valor* es 0, 1 o 2. Para volver a darle el valor predeterminado de marcapasos administrar el parámetro, ejecute la misma instrucción no tiene ningún valor.

Conmutación automática por error de un grupo de disponibilidad es posible cuando se cumplen las condiciones siguientes:

-   El servidor principal y la réplica secundaria se establecen en el movimiento de datos sincrónica.
-   La base de datos secundaria tiene un estado sincronizado (no sincronizar), lo que significa que los dos están en el mismo punto de datos.
-   El tipo de clúster está establecido como externo. Conmutación automática por error no es posible con un tipo de clúster de None.
-   El `sequence_number` de la réplica secundaria se convierta en el servidor principal tiene el número de secuencia superior: en otras palabras, la réplica secundaria `sequence_number` coincide con la de la réplica principal original.

Si se cumplen estas condiciones y se produce un error en el servidor que hospeda la réplica principal, el AG cambiará la propiedad a una réplica sincrónica. El comportamiento de réplicas sincrónicas (de lo que puede haber tres total: uno principal y dos réplicas secundarias) puede controlarse aún más mediante `required_synchronized_secondaries_to_commit`. Esto funciona con grupos de disponibilidad en Windows y Linux, pero se configura de forma totalmente diferente. En Linux, el valor se configura automáticamente el clúster en el propio recurso de AG.

## <a name="configuration-only-replica-and-quorum"></a>Quórum y la réplica solo configuración

También nuevo en [!INCLUDE[sssql17-md](../includes/sssql17-md.md)] en CU1 es una réplica de solo configuración. Porque marcapasos es diferente de un WSFC, especialmente cuando se trata de quórum y la necesidad de STONITH, con una configuración de dos nodos no funcionará cuando se trata de un AG. Una FCI, los mecanismos de quórum proporcionados por marcapasos pueden ser un problema, porque todos los arbitraje de conmutación por error FCI ocurre en el nivel de clúster. Para un AG, arbitraje en Linux ocurre en [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)], donde se almacenan todos los metadatos. Se trata en la réplica de solo configuración entra en juego.

Sin nada más, un tercer nodo y al menos una réplica sincronizada sería necesarios. Esto podría no funcionar [!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)], ya que sólo puede tener dos réplicas que participan en un AG. La réplica de solo configuración almacena la configuración de AG en la base de datos maestra, igual que las otras réplicas en la configuración de AG. La réplica de solo configuración no tiene las bases de datos de usuario que participa en el AG. Los datos de configuración se envían de forma sincrónica desde el servidor principal. Estos datos de configuración, a continuación, se usan durante las conmutaciones por error, independientemente de si están automático o manual.

Para que un AG mantener quórum y habilitar la conmutación automática por error con un tipo de clúster de externo, ya sea debe:

-   Tiene tres réplicas sincrónicas ([!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)] solo); o
-   Tener dos réplicas (principales y secundaria), así como una única réplica de configuración.

Las conmutaciones por error manual pueden ocurrir si se está utilizando externo o ninguno tipos para las configuraciones de AG del clúster. Aunque una réplica de configuración solo se puede configurar con un AG que tiene un tipo de clúster de None, no se recomienda, ya que complica la implementación. Para esas configuraciones, modificar manualmente `required_synchronized_secondaries_to_commit` tenga un valor de al menos 1, por lo que hay al menos una réplica sincronizada.

Una réplica de configuración solo se puede hospedar en cualquier edición de [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)], incluido [!INCLUDE[ssexpress-md](../includes/ssexpress-md.md)]. Esto minimizará los costos de licencia y se asegura de funciona con grupos de disponibilidad en [!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)]. Esto significa que la tercera necesita server solo se tiene que cumplir con las especificaciones mínimas para [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)], ya que no está recibiendo tráfico de transacciones de usuario de disponibilidad.

Cuando se usa una réplica de solo configuración, tiene el siguiente comportamiento:

-   De forma predeterminada, `required_synchronized_secondaries_to_commit` se establece en 0. Esto puede modificarse de forma manual en 1 si lo desea.
-   Si se produce un error en el servidor principal y `required_synchronized_secondaries_to_commit` es 0, la réplica secundaria se convertirá en el nuevo elemento principal y esté disponible para lectura y escritura. Si el valor es 1, se producirán conmutación automática por error, pero no aceptará las nuevas transacciones hasta que la otra réplica está en línea.
-   Si se produce un error en una réplica secundaria y `required_synchronized_secondaries_to_commit` es 0, la réplica principal sigue aceptando las transacciones, pero si el servidor principal produce un error en este momento, no hay ninguna protección para los datos ni la conmutación por error posible (manual o automático), ya que una réplica secundaria no está disponible.
-   Si se produce un error en las réplicas solo configuración, disponibilidad seguirán funcionando con normalidad, pero no es posible conmutación automática por error.
-   Si una réplica secundaria sincrónica y la réplica de solo configuración produce un error, el servidor principal no puede aceptar las transacciones, y no hay ningún destino principal no se pueda.

En CU1 hay un problema conocido en el registro en el archivo corosync.log que se genera a través de `mssql-server-ha`. Si una réplica secundaria no puede convertirse en el servidor principal debido al número de réplicas necesarios disponibles, el mensaje actual dice "esperan recibir números de secuencia 1 pero se recibieron solo 2. No hay suficientes réplicas están en línea con seguridad promover la réplica local." Se deben invertir los números, y debe indicar "esperan recibir 2 números de secuencia pero se recibieron solo 1. No hay suficientes réplicas están en línea con seguridad promover la réplica local." 

## <a name="multiple-availability-groups"></a>Varios grupos de disponibilidad 

Se puede crear más de un grupo de disponibilidad por clúster marcapasos o conjunto de servidores. La única limitación es que los recursos del sistema. Propiedad AG se muestra el maestro. Pueden ser propiedad de distintos grupos de disponibilidad en nodos diferentes; No todas deben estar ejecutándose en el mismo nodo.

## <a name="drive-and-folder-location-for-databases"></a>Ubicación de unidad y la carpeta de bases de datos

Como en grupos de disponibilidad basados en Windows, la estructura de la unidad y la carpeta para las bases de datos de usuario que participa en un AG debe ser idéntica. Por ejemplo, si las bases de datos de usuario se encuentran en `/var/opt/mssql/userdata` en el servidor A, esa misma carpeta debe existir en el servidor B. La única excepción a esto se indica en la sección [interoperabilidad con grupos de disponibilidad basados en Windows y las réplicas](#interoperability-with-windows-based-availability-groups-and-replicas).

## <a name="the-listener-under-linux"></a>El agente de escucha en Linux

El agente de escucha es una funcionalidad opcional para un AG. Proporciona un único punto de entrada para todas las conexiones (lectura/escritura a la réplica principal o a réplicas de solo lectura a secundaria) para que las aplicaciones y los usuarios finales no es necesario saber qué servidor hospeda los datos. En un WSFC, esto es la combinación de un recurso de nombre de red y un recurso IP, que, a continuación, se registra en AD DS (si es necesario), así como de DNS. En combinación con el propio recurso de AG, proporciona esa abstracción. Para obtener más información sobre un agente de escucha, vea [los agentes de escucha, conectividad de cliente y conmutación por error de aplicación](../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md).

El agente de escucha en Linux se configura de manera diferente, pero su funcionalidad es la misma. No hay ningún concepto de un recurso de nombre de red en marcapasos ni se crea un objeto en AD DS; hay solo un recurso de dirección IP creado en marcapasos que se pueden ejecutar en cualquiera de los nodos. Se debe crear una entrada asociada al recurso IP para el agente de escucha en DNS con un "nombre descriptivo". El recurso IP para el agente de escucha sólo estará activo en el servidor que hospeda la réplica principal de ese grupo de disponibilidad.

Si se utilizan marcapasos y se crea un recurso de dirección IP que está asociado con el agente de escucha, habrá una breve interrupción tal y como la dirección IP se detiene en un servidor y se inicia en el otro, ya sea la conmutación por error automática o manual. Si bien proporciona abstracción por medio de la combinación de un nombre único y la dirección IP, no se enmascara la interrupción. Una aplicación debe ser capaz de controlar la desconexión debido a algún tipo de funcionalidad detectarlo y volver a conectarse.

Sin embargo, la combinación del nombre DNS y dirección IP es todavía no hay suficientes para proporcionar toda la funcionalidad que proporciona un agente de escucha en un WSFC, como el enrutamiento de solo lectura para las réplicas secundarias. Al configurar un AG, una "escucha" aún debe configurarse en [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]. Esto puede verse en el asistente, así como la sintaxis de Transact-SQL. Hay dos formas de que esto puede configurarse para que funcione igual que en Windows:

-   Para un grupo de disponibilidad con un tipo de clúster de externo, la dirección IP asociada con la "escucha" que creó en [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] debe ser la dirección IP del recurso creado en marcapasos.
-   Para un AG creado con un tipo de clúster de None, use la dirección IP asociada con la réplica principal.

La instancia asociada con la dirección IP proporcionada a continuación, se convierte en el coordinador para cosas como las solicitudes de enrutamientos de solo lectura de aplicaciones.

## <a name="interoperability-with-windows-based-availability-groups-and-replicas"></a>Interoperabilidad con grupos de disponibilidad basados en Windows y réplicas 

Un AG que tiene un tipo de clúster de externo o uno que sea WSFC no puede tener sus réplicas entre plataformas. Esto es cierto si el AG es [!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)] o [!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)]. Esto significa que en una configuración AG tradicional con un clúster subyacente, no puede ser una réplica en un WSFC y el otro en Linux con marcapasos.

Un AG con un tipo de clúster de ninguno puede tener sus réplicas cruzar los límites de sistema operativo, por lo que podría haber ambas réplicas basadas en Windows y Linux en el mismo AG. A continuación se muestra un ejemplo donde la réplica principal está basado en Windows, mientras que la base de datos secundaria se encuentra en una de las distribuciones de Linux.

![Híbrido ninguno](./media/sql-server-linux-availability-group-overview/image1.png)

Un grupo de disponibilidad distribuido también puede cruzar los límites de sistema operativo. Los grupos de disponibilidad subyacentes están enlazados mediante las reglas de cómo estén configuradas, por ejemplo, una configurada con externo está solo Linux, pero el AG que se ha unido a podría configurarse con un WSFC. Considere el ejemplo siguiente:

![Híbrido Dist AG](./media/sql-server-linux-availability-group-overview/image2.png)

<!-- Distributed AGs are also supported for upgrades from [!INCLUDE[sssql15-md](../includes/sssql15-md.md)] to [!INCLUDE[sssql17-md](../includes/sssql17-md.md)]. For more information on how to achieve this, see [the article “x”].

If using automatic seeding with a distributed availability group that crosses OSes, it can handle the differences in folder structure. How this works is described in [the documentation for automatic seeding].
-->
 
## <a name="next-steps"></a>Pasos siguientes
[Configurar grupo de disponibilidad para SQL Server en Linux](sql-server-linux-availability-group-configure-ha.md)

[Configurar grupo de disponibilidad de la escala de lectura para SQL Server en Linux](sql-server-linux-availability-group-configure-rs.md)

[Agregar grupo de disponibilidad recurso de clúster en RHEL](sql-server-linux-availability-group-cluster-rhel.md)

[Agregar grupo de disponibilidad recurso de clúster en SLES](sql-server-linux-availability-group-cluster-sles.md)

[Agregar grupo de disponibilidad recurso de clúster en Ubuntu](sql-server-linux-availability-group-cluster-ubuntu.md)

[Configurar un grupo de disponibilidad entre plataformas](sql-server-linux-availability-group-cross-platform.md)

