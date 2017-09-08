---
title: SQL Server Integration Services (SSIS) escalada Support for High Availability | Documentos de Microsoft
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: 1
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 2405235bcfa09d2cc49e007f4eae6975d9ebf7a5
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="scale-out-support-for-high-availability"></a>Compatibilidad horizontalmente para alta disponibilidad

En SSIS horizontalmente, es proporcionar alta disponibilidad de lado de trabajo a través de ejecutar paquetes con varios escala Out trabajadores.
Lado maestro de alta disponibilidad se logra con [Always On para el catálogo de SSIS](../service/ssis-catalog.md#always-on-for-ssis-catalog-ssisdb) y clúster de conmutación por error de Windows. Varias instancias de escala Out Master se hospedan en un clúster de conmutación por error de Windows. Cuando el servicio de escala Out Master o SSISDB está desactivado en el nodo principal, el servicio o SSISDB en el nodo secundario continuarán aceptará las solicitudes de usuario y comunicarse con los trabajadores de salida de escala. 

Para configurar la alta disponibilidad de lado maestro, siga estos pasos.

## <a name="1-prerequisites"></a>1. Requisitos previos
Configure un clúster de conmutación por error de Windows. Consulte la entrada de blog [Installing the Failover Cluster Feature and Tools for Windows Server 2012](http://blogs.msdn.com/b/clustering/archive/2012/04/06/10291601.aspx) (Instalación de las herramientas y la característica de clúster de conmutación por error para Windows Server 2012) a fin de obtener instrucciones. Debe instalar la característica y las herramientas en todos los nodos del clúster.

## <a name="2-install-scale-out-master-on-primary-node"></a>2. Instalar a escala Out maestra en el nodo principal
Instalar servicios de motor de base de datos, Integration Services y escala Out maestro en el nodo principal para escala Out Master. 

Durante la instalación, debe 
### <a name="21-set-the-account-running-scale-out-master-service-to-a-domain-account"></a>2.1 establecer la cuenta que ejecuta el servicio escala Out maestro para una cuenta de dominio.
Esta cuenta debe ser capaz de obtener acceso a SSISDB en el nodo secundario en el clúster de conmutación por error de Windows en el futuro. Como servicio escala Out maestro y SSISDB pueden por separado de la conmutación por error, que no estén en el mismo nodo.

![Configuración del servidor de alta disponibilidad](media/ha-server-config.PNG)

### <a name="22-include-scale-out-master-service-dns-host-name-in-the-cns-of-scale-out-master-certificate"></a>2.2 incluyen escala Out Master nombre DNS del servicio host en el certificado de CNs de escala Out principal.

Este nombre de host se usará en el punto de conexión de escala Out Master. 

![Configuración principal de alta disponibilidad](media/ha-master-config.PNG)

## <a name="3-install-scale-out-master-on-secondary-node"></a>3. Instalar a escala Out maestra en el nodo secundario
Instalar servicios de motor de base de datos, Integration Services y escala Out maestro en el nodo secundario para escala Out Master. 

Debe utilizar el mismo certificado de escala Out maestra con el nodo principal. Exportar el certificado SSL de escala Out maestra en el nodo principal con clave privada e instalarlo en el almacén de certificados raíz de la máquina de loacl en el nodo secundario. Seleccionar este certificado al instalar a escala Out Master.

![Configuración de alta disponibilidad maestro 2](media/ha-master-config2.PNG)

> [!Note]
> Puede establecer la copia de seguridad de varios maestros fuera de la escala mediante la repetición de las operaciones de escala secundaria Out Master.

## <a name="4-set-up-ssisdb-always-on"></a>4. Configurar siempre SSISDB en

Las instrucciones para configurar siempre en para SSISDB puede verse en [Always On para el catálogo de SSIS (SSISDB)](../service/ssis-catalog.md#always-on-for-ssis-catalog-ssisdb).

Además, debe crear un agente de escucha de gourp de disponibilidad para el grupo de disponibilidad A que SSISDB agregado. Vea [crear o configurar un agente de escucha del grupo de disponibilidad](../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md).

## <a name="5-update-scale-out-master-service-configuration-file"></a>5. Archivo de configuración de servicio de actualización escala Out Master
Archivo de configuración del servicio de actualización escala Out Master, \<controlador\>: \Program Server\140\DTS\Binn\MasterSettings.config SQL, en los nodos principales y secundarios. Actualización **SqlServerName** a *[nombre de DNS de agente de escucha del grupo de disponibilidad], [puerto]*.

## <a name="6-enable-package-execution-logging"></a>6. Habilitar el registro de ejecución del paquete

Inicio de sesión SSISDB se realiza mediante el inicio de sesión **MS_SSISLogDBWorkerAgentLogin ##**, cuya contraseña es generados automáticamente. Para que funciona el registro para todas las réplicas de SSISDB, realice lo siguiente.

### <a name="61-change-the-password-of-msssislogdbworkeragentlogin-on-primary-sql-server"></a>6.1 cambiar la contraseña de **MS_SSISLogDBWorkerAgentLogin ##** en Sql Server principal.
### <a name="62-add-the-login-to-secondary-sql-server"></a>6.2 Agregue el inicio de sesión a Sql Server secundario.
### <a name="63-update-connection-string-of-logging"></a>6.3 actualizar la cadena de conexión del registro.
Llame al procedimiento almacenado [catalog]. [update_logdb_info] con 

@server_name= '*[Nombre de DNS de agente de escucha del grupo de disponibilidad], [puerto]*' 

y @connection_string = ' origen de datos =*[nombre de DNS de agente de escucha del grupo de disponibilidad]*,*[puerto]*; Initial Catalog = SSISDB; Id. de usuario = MS_SSISLogDBWorkerAgentLogin ##; Contraseña =*[Password]*];'.

## <a name="7-congifure-scale-out-master-service-role-of-windows-failover-cluster"></a>7. Escala Out Master de configurar el rol de servicio de clúster de conmutación por error de Windows

Conmutación por error de conmutación por error, conéctese al clúster de escala de salida. Seleccione el clúster y haga clic en **acción** en el menú y, a continuación, **configurar rol...** .

En el texto extraído seguridad **Asistente para alta disponibilidad**, seleccione **servicio genérico** en **Seleccionar rol** página y elija SQL Server Integration Services escala Out Master 14.0 en **Seleccionar servicio** página.

En el **punto de acceso de cliente** página, escriba el nombre de host DNS del servicio de escala Out Master.

![Alta disponibilidad Asistente 1](media/ha-wizard1.PNG)

Finalice al asistente.

## <a name="8-update-master-address-in-ssisdb"></a>8. Actualizar Master dirección en SSISDB

En el servidor principal de SQL, ejecute el procedimiento almacenado [SSIS]. [catalog]. [update_master_address] con el parámetro @MasterAddress = N'https: / / [nombre de host DNS del servicio de escala Out Master]: [puerto Master]'. 

## <a name="9-add-scale-out-worker"></a>9. Agregar escalada de trabajo

Ahora, puede agregar escala espera trabajos con la Ayuda de [escala Out Manager](integration-services-ssis-scale-out-manager.md). Escriba *[nombre de DNS de agente de escucha de grupo disponibilidad de SQL Server]*,*[puerto]* en la página de conexión.





