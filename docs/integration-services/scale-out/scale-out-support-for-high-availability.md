---
title: Compatibilidad con la escalabilidad horizontal de SQL Server Integration Services (SSIS) para una alta disponibilidad | Microsoft Docs
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: scale-out
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: "1"
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2202b61a9efce26edb0edcef53204351338ecee6
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="scale-out-support-for-high-availability"></a>Compatibilidad con la escalabilidad horizontal para una alta disponibilidad

En la escalabilidad horizontal de SSIS, la alta disponibilidad del trabajo se proporciona a través de la ejecución de paquetes con varios trabajos de escalabilidad horizontal.
La alta disponibilidad del patrón se logra con [Always On para el catálogo de SSIS](../service/ssis-catalog.md#always-on-for-ssis-catalog-ssisdb) y el clúster de conmutación por error de Windows. Varias instancias del patrón de escalabilidad horizontal se hospedan en un clúster de conmutación por error de Windows. Si el servicio de patrón de escalabilidad horizontal o SSISDB están desactivados en el nodo principal, el servicio o SSISDB en el nodo secundario continuarán aceptando solicitudes de usuario y comunicándose con los trabajos de escalabilidad horizontal. 

Para configurar la alta disponibilidad del patrón, realice los pasos siguientes.

## <a name="1-prerequisites"></a>1. Requisitos previos
Configure un clúster de conmutación por error de Windows. Consulte la entrada de blog [Installing the Failover Cluster Feature and Tools for Windows Server 2012](http://blogs.msdn.com/b/clustering/archive/2012/04/06/10291601.aspx) (Instalación de las herramientas y la característica de clúster de conmutación por error para Windows Server 2012) a fin de obtener instrucciones. Debe instalar la característica y las herramientas en todos los nodos del clúster.

## <a name="2-install-scale-out-master-on-primary-node"></a>2. Instalar el patrón de escalabilidad horizontal en el nodo principal
Instale Servicios de Motor de base de datos, Integration Services y el patrón de escalabilidad horizontal en el nodo principal del patrón de escalabilidad horizontal. 

Durante la instalación, debe 
### <a name="21-set-the-account-running-scale-out-master-service-to-a-domain-account"></a>2.1 Establecer la cuenta que ejecuta el servicio del patrón de escalabilidad horizontal en una cuenta de dominio.
Esta cuenta debe ser capaz de acceder a SSISDB en el nodo secundario del clúster de conmutación por error de Windows en el futuro. Dado que la comutación por error del servicio del patrón de escalabilidad y de SSISDB se puede realizar por separado, es posible que no estén en el mismo nodo.

![Configuración del servidor HA](media/ha-server-config.PNG)

### <a name="22-include-scale-out-master-service-dns-host-name-in-the-cns-of-scale-out-master-certificate"></a>2.2 Incluir el nombre de host DNS del servicio del patrón de escalabilidad horizontal en los nombres comunes del certificado del patrón de escalabilidad horizontal.

Este nombre de host se usará en el punto de conexión del patrón de escalabilidad horizontal. 

![Configuración del patrón HA](media/ha-master-config.PNG)

## <a name="3-install-scale-out-master-on-secondary-node"></a>3. Instalar el patrón de escalabilidad horizontal en el nodo secundario
Instale Servicios de Motor de base de datos, Integration Services y el patrón de escalabilidad horizontal en el nodo secundario del patrón de escalabilidad horizontal. 

Debe usar el mismo certificado del patrón de escalabilidad horizontal con el nodo principal. Exporte el certificado SSL del patrón de escalabilidad horizontal en el nodo principal con clave privada e instálelo en el almacén de certificados raíz de la máquina local en el nodo secundario. Seleccione este certificado cuando instale el patrón de escalabilidad horizontal.

![Configuración del patrón HA 2](media/ha-master-config2.PNG)

> [!Note]
> Puede configurar varios patrones de escalabilidad horizontal de copia de seguridad mediante la repetición de las operaciones del patrón de escalabilidad horizontal secundaria.

## <a name="4-set-up-ssisdb-always-on"></a>4. Configurar Always On de SSISDB

Las instrucciones para configurar Always On para SSISDB pueden consultarse en [Always On para el catálogo de SSIS (SSISDB)](../service/ssis-catalog.md#always-on-for-ssis-catalog-ssisdb).

Además, debe crear un agente de escucha de grupo de disponibilidad para SSISDB del grupo de disponibilidad agregado. Consulte [Create or Configure an Availability Group Listener](../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md) (Crear o configurar un agente de escucha de grupo de disponibilidad).

## <a name="5-update-scale-out-master-service-configuration-file"></a>5. Actualizar el archivo de configuración del servicio del patrón de escalabilidad horizontal
Actualice el archivo de configuración del servicio del patrón de escalabilidad horizontal, \<unidad\>:\Archivos de programa\Microsoft SQL Server\140\DTS\Binn\MasterSettings.config, en los nodos principal y secundario. Actualice **SqlServerName** a *[Nombre DNS del agente de escucha de grupo de disponibilidad],[Puerto]*.

## <a name="6-enable-package-execution-logging"></a>6. Habilitar el registro de la ejecución de paquetes

El registro en SSISDB se realiza mediante el inicio de sesión **##MS_SSISLogDBWorkerAgentLogin##**, cuya contraseña se genera automáticamente. Para que el registro funcione para todas las réplicas de SSISDB, realice las siguientes acciones.

### <a name="61-change-the-password-of-msssislogdbworkeragentlogin-on-primary-sql-server"></a>6.1 Cambiar la contraseña de **##MS_SSISLogDBWorkerAgentLogin##** en la instancia de SQL Server principal.
### <a name="62-add-the-login-to-secondary-sql-server"></a>6.2 Agregar el inicio de sesión a la instancia de SQL Server secundaria.
### <a name="63-update-connection-string-of-logging"></a>6.3 Actualizar la cadena de conexión del registro.
Llame al procedimiento almacenado [catalog].[update_logdb_info] con 

@server_name = '*[Nombre DNS del agente de escucha de grupo de disponibilidad],[Puerto]*'. 

y @connection_string = 'Data Source=*[Nombre DNS del agente de escucha de grupo de disponibilidad]*,*[Puerto]*;Initial Catalog=SSISDB;User Id=##MS_SSISLogDBWorkerAgentLogin ##;Password=*[Contraseña]*];'.

## <a name="7-congifure-scale-out-master-service-role-of-windows-failover-cluster"></a>7. Configurar el rol de servicio del patrón de escalabilidad horizontal del clúster de conmutación por error de Windows

En el Administrador de clústeres de conmutación por error, conéctese al clúster de escalabilidad horizontal. Seleccione el clúster y haga clic en **Acción** en el menú. A continuación, seleccione **Configurar rol...**.

En el **Asistente para alta disponibilidad** que aparece, seleccione **Servicio genérico** en la página **Seleccionar rol** y elija SQL Server Integration Services Scale Out Master 14.0 en la página **Seleccionar servicio**.

En la página **Punto de acceso de cliente**, escriba el nombre de host DNS del servicio de patrón de escalabilidad horizontal.

![Asistente HA 1](media/ha-wizard1.PNG)

Finalice al asistente.

## <a name="8-update-master-address-in-ssisdb"></a>8. Actualizar la dirección del patrón en SSISDB

En el servidor principal de SQL Server, ejecute el procedimiento almacenado [SSIS].[catalog].[update_master_address] con el parámetro @MasterAddress = N'https://[nombre de host DNS del servicio de patrón de escalabilidad horizontal]:[Puerto maestro]'. 

## <a name="9-add-scale-out-worker"></a>9. Agregar el trabajo de escalabilidad horizontal

Ahora, puede agregar trabajos de escalabilidad horizontal con la ayuda del [Administrador de escalabilidad horizontal](integration-services-ssis-scale-out-manager.md). Escriba *[Nombre DNS del agente de escucha de grupo disponibilidad de SQL Server]*,*[Puerto]* en la página de conexión.




