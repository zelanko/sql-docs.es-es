---
title: "Alta disponibilidad y recuperación ante desastres para Master Data Services | Documentos de Microsoft"
ms.custom:
- SQL2016_New_Updated
ms.date: 07/28/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 
caps.latest.revision: 
author: sabotta
ms.author: carlasab
manager: craigg
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 2afbf59101a0605dba2e79f09777160cb4de5cab
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---



# <a name="high-availability-and-disaster-recovery-for-master-data-services"></a>Alta disponibilidad y recuperación ante desastres para Master Data Services

**Resumen:** en este artículo se describe una solución para la configuración de Master Data Service (MDS) hospedado en un grupo de disponibilidad AlwaysOn. En el artículo se describe cómo instalar y configurar SQL 2016 Master Data Services en un grupo de disponibilidad (AG) AlwaysOn de SQL 2016. El propósito principal de esta solución es mejorar la alta disponibilidad y la recuperación ante desastres de datos de back-end MDS hospedados en una base de datos de SQL Server.

## <a name="introduction"></a>Introducción


Este artículo describe una solución para el servicio de datos maestra (MDS) hospedado en una configuración de grupo de disponibilidad AlwaysOn. El artículo describe cómo instalar y configurar SQL 2016 MDS en un grupo de disponibilidad de SQL 2016 AlwaysOn (AG). El propósito principal de esta solución es mejorar la alta disponibilidad y la recuperación ante desastres de datos de back-end MDS hospedados en una base de datos de SQL Server.

Para implementar la solución, debe completar las siguientes tareas que se describen en este artículo.

1.  [Instale y configure el clúster de conmutación por error de Windows Server (WSFC)](#windows-server-failover-cluster-wsfc).

2.  [Configurar AlwaysOn AG](#sql-server-alwayson-availability-group).

3.  [Configurar MDS se ejecute en un nodo WSFC](#configure-mds-to-run-on-an-wsfc-node).

En las secciones anteriores, se impondrán brevemente las tecnologías, seguidas de las instrucciones. Para obtener información detallada acerca de las tecnologías, revise los documentos que se indican en cada sección.

Esta solución que se describe en este artículo se basa en SQL Server AlwaysOn AG, en la que cada base de datos tiene varias réplicas sincrónicas o asincrónicas. Una única réplica acepta la transacción (acepta las solicitudes del usuario). Se trata de la réplica principal.

Cada réplica tiene su propio almacenamiento, por lo que no hay ningún almacenamiento compartido centralizado en esta solución. Cuando se produce un error de software o un error de hardware que afectan a la réplica principal, la réplica principal puede conmutar por error a una réplica sincrónica o asincrónica automática o manualmente se basa en la configuración y situaciones. Esto garantiza la alta disponibilidad de la base de datos con una interrupción mínima para los usuarios.

Las réplicas asincrónicas normalmente se hospedan en un centro de datos remoto desde el centro de datos de la réplica principal. En el caso de escenarios de desastre, la réplica principal puede conmutar por error a otro centro de datos. Esto garantiza la recuperación ante desastres de la base de datos.

Con fines de demostración, la solución descrita en este artículo usa las siguientes versiones de software. Las versiones anteriores deben funcionar lo mismo con potencialmente pequeñas diferencias.

-   Windows Server 2012 R2 con el clúster de conmutación por error de servidor

-   SQL Server 2016 con la característica de Master Data Services

Además, la solución utiliza dos máquinas virtuales, **MDS HA1** y **MDS HA2**, hospedar dos réplicas. Siempre y cuando es compatible con SQL Server AlwaysOn AG, MDS no limitar cuántas réplicas que se puede usar.

En este artículo se da por supuesto que tiene conocimientos básicos sobre Windows Server, clúster de conmutación por error de Windows Server, SQL Server AlwaysOn y MDS de SQL Server.

## <a name="what-is-not-covered"></a>Lo que no está cubierto

Este documento no cubre lo siguiente:

-   Cómo hacer que IIS, el servidor de web que hospeda el maestro de interfaz de usuario, puede recuperar después de un desastre y de alta disponibilidad del servicio de datos. MDS no impone ningún requisito concreto en IIS, por lo que las técnicas estándares para que IIS tenga alta disponibilidad y equilibrio de carga pueden utilizar aquí también.

-   Describe cómo usar el clúster de conmutación por error (FCI) de SQL Server AlwaysOn para admitir alta disponibilidad (HA) en el servidor MDS. Agrupación en clústeres de conmutación por error de SQL Server es una solución de alta disponibilidad diferentes y es compatible oficialmente con SQL Server, y trabajar con MDS.

-   Describe cómo usar una solución híbrida de clúster de conmutación por error de SQL Server (FCI) y AlwaysOn AG para admitir alta disponibilidad en el servidor MDS. ¿Funciona la solución híbrida con MDS.

## <a name="design-consideration"></a>Consideración de diseño

Figura 1 muestra una configuración típica que se usa principalmente en AlwaysOn AG. En el centro de datos principal, hay dos réplicas con una relación de confirmación sincrónica y ambas réplicas tienen el privilegio de voto. Se utiliza principalmente para mejorar la alta disponibilidad en caso de que se produce un error en la réplica principal.

En el centro de datos de recuperación ante desastres, hay una réplica secundaria con una relación de confirmación asincrónica con la principal. Este centro de datos suele ser en una región geográfica diferente que el centro de datos principal. La réplica secundaria no tiene privilegios de voto.

Esta configuración se utiliza para lograr la recuperación en caso de que el centro de datos principal está en un desastre, como un incendio, terremoto, etcetera. La configuración logra ambos alta disponibilidad y recuperación ante desastres con un costo relativamente bajo.

![Configuración típica para el grupo de disponibilidad AlwaysOn](media/Fig1_TypicalConfig.png)

Figura 1. Una configuración de grupo de disponibilidad AlwaysOn típico

Si no tiene que considere la posibilidad de recuperación ante desastres, no es necesario tener una réplica en un segundo centro de datos. Si necesita para mejorar la alta disponibilidad, podría tener varias réplicas sincrónicas en el mismo centro de datos principal con.

Por lo que es importante tener en cuenta los escenarios y requisitos y elegir cuántas réplicas sincrónicas y asincrónicas necesita y qué centro de datos debe colocar en.

## <a name="windows-server-failover-cluster-wsfc"></a>Clúster de conmutación por error de Windows Server (WSFC)

Esta sección tratan las siguientes tareas.

1.  [Instalar la característica clúster de conmutación por error de Windows](#install-failover-cluster-feature).

2.  [Crear un clúster de conmutación por error de Windows Server](#create-a-windows-server-failover-cluster).

Como se muestra en la figura 1 en la sección anterior, la solución descrita en este artículo incluye el clúster de conmutación por error de Windows Server (WSFC). Es necesario configurar WSFC porque AlwaysOn de SQL depende WFSC conmutación por error y la detección de errores.

WSFC es una característica para mejorar la alta disponibilidad de aplicaciones y servicios. Consta de un grupo de instancias de servidor de windows independiente con el servicio de clúster de conmutación por error de Microsoft con esas instancias. Las instancias de servidor de windows (o nodos como se denominan a veces) está conectado para que puedan comunicarse entre sí y la detección de errores es posible. WSFC proporciona las funcionalidades de detección y conmutación por error de error. Si un nodo o un servicio produce un error en el clúster, a continuación, se detecta el error y otro nodo de forma automática o manual empieza a proporcionar los servicios alojados en el nodo con error. Por lo tanto, los usuarios solo experimentan interrupciones mínimas en los servicios, y se mejora la disponibilidad del servicio.  

### <a name="prerequisites"></a>Requisitos previos

El sistema operativo Windows Server está instalado en todas las instancias y todas las actualizaciones se han modificado.

>[!NOTE] 
>Es **recomienda** instalar la misma versión de Windows y el mismo conjunto en todas las instancias para evitar posibles problemas de incompatibilidad de características.

### <a name="install-failover-cluster-feature"></a>Instalar la característica clúster de conmutación por error

Complete los pasos siguientes para cada instancia del servidor de Windows instalar la característica WSFC en cada instancia. Necesita permisos de administrador.

1.  Abra **el administrador del servidor** en Windows Server y haga clic en **agregar Roles y características** en el panel derecho. Se iniciará el **agregar Roles y características Asistente**.

2.  Haga clic en **siguiente** hasta llegar a la **características** página.

3.  Seleccione el **agrupación en clústeres de conmutación por error** casilla de verificación y, a continuación, haga clic en **siguiente** para finalizar la instalación. Consulte la figura 2.

    Si le pide confirmación para **agregar características requeridas para la agrupación en clústeres de conmutación por error**, haga clic en **agregar características**. Consulte la figura 3.

    ![Agregar Roles y características Asistente, agrupación en clústeres de conmutación por error](media/Fig2_SelectFeatures.png)

    Figura 2

    ![Agregar Roles y características Asistente, necesarios para el clúster de conmutación por error](media/Fig3_RequiredFeaturesFailover.png)

    Figura 3

4.  En el **confirmación** página, haga clic en **instalar** para instalar la característica de clústeres de conmutación por error.

5.  En el **resultado** página, asegúrese de que todo se ha instalado correctamente sin errores y advertencias.

### <a name="create-a-windows-server-failover-cluster"></a>Crear un clúster de conmutación por error de Windows Server

Después de instala la característica WSFC en todas las instancias, puede configurar WSFC. Solo es necesario hacer esto en un nodo.

1.  Abra **el administrador del servidor** en Windows Server y haga clic en **Administrador de clústeres de conmutación por error** en el **herramienta** menú situado en la esquina superior derecha para iniciar el administrador.

2.  En **Administrador de clústeres de conmutación por error**, haga clic en **validar configuración** en el panel derecho. Consulte la figura 4.

    ![Administrador de clústeres de conmutación por error, validar configuración](media/Fig4_ValidateConfig.png)

    Figura 4

3.  En el **validar una configuración** **asistente**, haga clic en **siguiente**.

4.  En el **seleccionar servidores o un clúster** diálogo cuadro, agregue los nombres de servidor que hospedan SQL Server y, a continuación, haga clic en **siguiente**. Consulte la figura 5.

    En este ejemplo se agregan dos instancias, MDS-HA1 y HA2 de MDS.

    ![Validar un asistente de configuración, seleccione servidores o una página de clúster](media/Fig5_AddServer.png)

    Figura 5

5.  En el **opciones de pruebas** página, haga clic en **ejecutar todas las pruebas**y, a continuación, haga clic en **siguiente**.

6.  Haga clic en **siguiente** para finalizar la validación.

    El **Validating** página muestra el progreso y la **resumen** página muestra el resumen de validación. Vea las figuras 6 y 7.

7.  En el **resumen** página, busque los mensajes de advertencia o error.

    Es preciso corregir errores. Sin embargo, las advertencias no pueden ser un problema. Un mensaje de advertencia significa que "el elemento probado puede cumplir el requisito, pero hay algo que debe comprobar". Por ejemplo, la figura 7 muestra un "latencia de acceso de disco validar" advertencia, que puede ser porque el disco está ocupado en otras tareas temporalmente y puede pasar por alto. Debe comprobar el documento en línea para cada advertencia y mensajes de error para obtener más detalles. Consulte la figura 7.
 
    ![Validar el Asistente para configuración, página validación](media/Fig6_ValidationTests.png)

    Figura 6

    ![Validar a un asistente de configuración, página Resumen](media/Fig7_ValidationSummary.png)

    Figura 7

8.  En el **resumen** página, confirme que la **crear el clúster ahora con los nodos validados** casilla de verificación está seleccionada y, a continuación, haga clic en **finalizar** para iniciar el **crear clúster** **asistente**.

9.  En el **crear clúster** **asistente**, haga clic en **siguiente**.

10. En el **punto de acceso para administrar el clúster** página, escriba el nombre del clúster WSFC y, a continuación, haga clic en **siguiente**. En este ejemplo, utilizamos "MDS-HA" como el nombre del clúster. Consulte la figura 8.

    ![Escriba el nombre del clúster](media/Fig8_EnterClusterName.png)

    Figura 8

11. Siga haciendo clic en **siguiente** para terminar de crear el clúster. El **resumen del clúster MDS-HA** sección muestra la información de clúster. Consulte la figura 9.

    ![Ver información de resumen para el clúster](media/Fig9_ClusterSummary.png)

    Figura 9

    Si necesita agregar un nodo más adelante, haga clic en **agregar nodo** acción en el panel derecho de **Administrador de clústeres de conmutación por error**.

Comentarios:

-   La característica WSFC no estén disponible en todas las ediciones de Windows Server. Asegúrese de que la edición tiene esta característica.

-   Asegúrese de que tiene los permisos adecuados para la instalación de WSFC en active directory. Si hay algún problema, consulte [guía paso a paso de clúster de conmutación por error: configurar cuentas en Active Directory](https://technet.microsoft.com/library/cc731002(v=ws.10).aspx).

Para obtener más información acerca de WSFC, vea [clústeres de conmutación por error](https://technet.microsoft.com/library/cc732488(v=ws.10).aspx).

## <a name="sql-server-alwayson-availability-group"></a>Grupo de disponibilidad AlwaysOn de SQL Server

Esta sección tratan las siguientes tareas.

1.  [Grupo de disponibilidad de habilitar SQL Server AlwaysOn](#enable-sql-server-alwayson-availability-group-on-every-sql-server-instance).

2.  [Crear un grupo de disponibilidad](#create-an-availability-group).

3.  [Validar y probar el grupo de disponibilidad](#validation-and-test-the-availability-group).

Soluciones de SQLServer AlwaysOn proporcionan alta disponibilidad y recuperación ante desastres para bases de datos de SQL Server. AlwaysOn tiene dos posibles soluciones.
Ambas se basan en WSFC.

-   Grupos de disponibilidad AlwaysOn (AG)

-   Instancias de clúster de conmutación por error de AlwaysOn (FCI).

AG mejora la alta disponibilidad de nivel de base de datos. El AG (un conjunto de bases de datos de usuario) y su nombre de red virtual se registran como recursos de WSFC.

FCI mejora la alta disponibilidad de nivel de instancia. Servicio SQL Server y los servicios relacionados se registran como recursos de WSFC. Además, la solución FCI requerirá almacenamiento de disco compartido simétrico, como SAN o SMB recursos compartidos de archivos, que debe estar disponible para todos los nodos del clúster de WFC.


### <a name="prerequisites"></a>Requisitos previos

-   Instalar a SQL Server en todos los nodos. Para obtener más información, vea [Instalar SQL Server 2016](https://docs.microsoft.com/sql/database-engine/install-windows/install-sql-server).

-   (Recomendado) Instale el exacta mismo conjunto de características de SQL Server y la versión en cada nodo. En concreto, MDS debe estar instalado.

-   (Recomendado) Utilice la misma configuración en cada instancia de SQL Server. En concreto, la misma intercalación de servidor debe configurarse en todas las instancias de SQL Server.

-   (Recomendado) Utilice la misma cuenta de servicio para ejecutar cada instancia de SQL Server. De lo contrario, tendrá que conceder permiso para cada instancia de SQL Server para asegurarse de que las instancias de SQL Server pueden comunicarse entre sí.

-   Confirme que la configuración de firewall de Windows permite que las instancias de SQL Server para comunicarse entre sí.

### <a name="enable-sql-server-alwayson-availability-group-on-every-sql-server-instance"></a>Habilitar grupo de disponibilidad de SQL Server AlwaysOn en cada instancia SQL Server

1.  En el **Administrador de configuración de SQL Server** haga clic en **servicio SQL Server** en el panel izquierdo, haga clic en **SQL Server** en el panel derecho y, a continuación, haga clic en **propiedades**. Consulte la figura 10.

    ![Ventana de propiedades de SQL Server](media/Fig10_SQLServerProperties.png)

    Figura 10

2.  En el **SQL Server (MSSQLSERVER)** **propiedades** cuadro de diálogo, haga clic en el **alta disponibilidad de AlwaysOn** pestaña y, a continuación, seleccione la **habilitar los grupos de disponibilidad AlwaysOn** casilla de verificación. Cuando se muestre un valor en el **nombre del clúster de conmutación por error de Windows** cuadro de texto, haga clic en **Aceptar** para continuar. Consulte la figura 11.

    ![Habilitar la opción de grupos de disponibilidad AlwaysOn](media/Fig11_EnableAlwaysOn.png)

    Figura 11

3.  Cuando se muestra una página de advertencia, haga clic en **Aceptar** para continuar. Consulte la figura 12.

    ![Confirmar para detener y reiniciar el servicio](media/Fig12_WarningServiceStopStart.png)

    Figura 12

4.  Haga clic en **reiniciar**, para reiniciar el **SQL Server** de servicio y que este cambio surta efecto. Consulte la figura 10.

>[!NOTE] 
>Puede cambiar la cuenta de servicio que se ejecuta el servicio de SQL Server utilizando la **Administrador de configuración de SQL Server**. Haga clic en el **iniciar sesión** pestaña en el **SQL Server (MSSQLSERVER)** **propiedades** cuadro de diálogo. Consulte la figura 11.

### <a name="create-an-availability-group"></a>Crear un grupo de disponibilidad

Después de habilita la característica AlwaysOn en todas las instancias de SQL Server, cree un nuevo AG que contiene la base de datos MDS en un nodo.

AG solamente puede crearse en bases de datos existentes. Lo mismo crear una base de datos MDS en un nodo, o crear una base de datos temporal y, a continuación, quitar la base de datos temporal. En este ejemplo, se crea una base de datos de emptyMDS y crea un AG en esta base de datos MDS.

1.  Iniciar **SQL Server Management Studio** (**SSMS**) en un nodo y conectarse a la instancia de SQL Server local con las credenciales adecuadas.

2.  En SSMS, abra un **nueva consulta** ventana y ejecute el siguiente script para crear una base de datos vacía. Reemplace C:\\temporal con la ubicación que desee utilizar para realizar una copia de seguridad completa.

    ```
    CREATE DATABASE MDS\_Sample
    GO
    BACKUP DATABASE MDS\_Sample TO DISK='C:\\temp'
    GO
    ```

    >[!NOTE] 
    >Una copia de seguridad completa de la base de datos es necesario para crear el AG en esta base de datos.

3.  En el **Explorador de objetos**, expanda la **alta disponibilidad de AlwaysOn** carpeta y haga clic en **el Asistente para nuevo grupo de disponibilidad** para iniciar el **el Asistente para nuevo grupo de disponibilidad**. Consulte la figura 13.

    ![Asistente para iniciar el nuevo grupo de disponibilidad](media/Fig13_AvailabilityGroupsFolder.png)

    Figura 13

4.  En el **nuevo grupo de disponibilidad** asistente, haga clic en **siguiente** para mostrar la **especificar el nombre** página. Escriba un nombre para la disponibilidad y, a continuación, haga clic en **siguiente**. Consulte la figura 14.

    ![Escriba el nombre del grupo de disponibilidad](media/Fig14_AvailabilityGroupName.png)

    Figura 14

5.  Haga clic en la base de datos que acaba de crear en el **Seleccionar base de datos** página y, a continuación, haga clic en **siguiente**. Consulte la figura 15.

    ![Seleccione la base de datos](media/Fig15_AvailabilityGroupSelectDatabase.png)

    Figura 15

6.  En el **especificar réplicas** página, agregue otra réplica, haga clic en **agregar una réplica**. Esta página ya enumera las instancias de SQL Server locales, actuales como una réplica. Consulte la figura 16.

7.  En el **conectar al servidor** diálogo cuadro, agregue las credenciales adecuadas y haga clic en **conectar**.

    ![Conectarse a una instancia de SQL Server](media/Fig16_AddReplicaConnectServer.png)

    Figura 16

    Ahora debería ver dos réplicas en la lista. Repita este paso para agregar otros nodos como réplicas. Consulte la figura 17.

    ![Ver la lista de réplicas](media/Fig17_AvailabilityGroupSQLReplicas.png)

    Figura 17

    Para cada réplica, configure las siguientes opciones **confirmación sincrónica**, **conmutación automática por error**, y **secundaria legible** configuración. Consulte la figura
17.

    **Confirmación sincrónica**: este modo se garantiza que si una transacción se confirma en la réplica principal de una base de datos, a continuación, la transacción también se confirma en todas las demás réplicas sincrónicas. Confirmación asincrónica no garantizar esto, y puede retrasarse detrás de la réplica principal.

    Normalmente debe habilitar la confirmación sincrónica solo cuando los dos nodos están en el mismo centro de datos. Si se encuentran en distintos centros de datos, confirmación sincrónica puede ralentizar el rendimiento de la base de datos.

    Si no se activa esta casilla, se utiliza la confirmación asincrónica.

    **Conmutación automática por error:** cuando la réplica principal está inactivo, el AG configurará automáticamente y de conmutación por error a su réplica secundaria cuando se selecciona la conmutación automática por error. Solo puede habilitarse en las réplicas con confirmaciones sincrónicas.

    **Base de datos secundaria legible:** de forma predeterminada, los usuarios no se pueden conectar a cualquier réplica secundaria. Esto le permitirá a los usuarios conectarse a la réplica secundaria con acceso de solo lectura.

8.  En el **especificar réplicas** página, haga clic en el **escucha** ficha y realice lo siguiente. Consulte la figura 18.

    A.  Haga clic en **crear un agente de escucha del grupo de disponibilidad** para configurar un agente de escucha del grupo de disponibilidad para la conexión de base de datos MDS.

    B.  Escriba un **nombre DNS del agente de escucha**, como MDSSQLServer.

    c.  Escriba el puerto SQL predeterminado, 1433, en la **puerto** cuadro de texto.

    d.  Escriba DHCP en el **modo de red** cuadro de texto y, a continuación, haga clic en **siguiente** para continuar.

    >[!NOTE] 
    >Si lo desea, puede elegir "IP estática" como el **modo de red** y escriba una dirección IP estática. También puede especificar un puerto distinto de 1433. 

    ![Configurar el agente de escucha](media/Fig18_AvailabilityGroupCreateListener.png)

    Figura 18

9.  En el **seleccionar sincronización de datos** página, haga clic en **completa**y especifique un recurso compartido de red que pueden tener acceso todos los nodos. Para continuar, haga clic en **Siguiente** . Consulte la figura 19.

    Este recurso compartido de red se utilizará para almacenar la copia de seguridad de base de datos para crear las réplicas secundarias. Si no está disponible para su organización, elija otra preferencia de sincronización de datos. Hacer referencia a [grupo de disponibilidad AlwaysOn de SQL Server 2016](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/always-on-availability-groups-sql-server) acerca de cómo usar otras opciones para crear réplicas secundarias. La figura 17 también muestra otras opciones.

    ![Configurar la sincronización de datos](media/Fig19_AvailabilityGroupDataSync.png)

    Figura 19 

10. En el **validación** página, asegúrese de que todas las validaciones se cumplieron correctamente y corrija los errores. Para continuar, haga clic en **Siguiente** .

11. En el **resumen** página, revise todos los valores de configuración y haga clic en **finalizar**. Esto creará el grupo de disponibilidad y configurarlo.

12. En el **resultado** página, confirme que se completaron todas las medidas necesarias.

### <a name="validation-and-test-the-availability-group"></a>El grupo de disponibilidad de comprobación y validación

1.  Abra SSMS y conectar con el nombre DNS del agente de escucha que acaba de crear en el [crear un grupo de disponibilidad](#create-an-availability-group) sección. En este ejemplo, es MDSSQLServer.

2.  En **Explorador de objetos**, expanda la **alta disponibilidad de AlwaysOn** carpeta, derecha haga clic en el AG recién creado en el [crear un grupo de disponibilidad](#create-an-availability-group) sección y, a continuación, haga clic en **Mostrar panel**. Véase la figura 20. Aparece el estado de disponibilidad nuevo y sus réplicas.

    ![Ver el panel](media/Fig20_ShowDashboard.png)

    Figura 20 

3.  Haga clic en **conmutación por error** para realizar una conmutación por error a una réplica sincrónica y una réplica asincrónica. Esto sirve para comprobar que conmutan por error se produce correctamente sin problemas.

 Se ha completado el programa de instalación de AlwaysOn.

Para obtener más información sobre el grupo de disponibilidad AlwaysOn, vea [grupo de disponibilidad AlwaysOn de SQL Server 2016](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/always-on-availability-groups-sql-server).

## <a name="configure-mds-to-run-on-an-wsfc-node"></a>Configurar MDS para ejecutarse en un nodo WSFC

Esta solución presentada en este artículo solo requiere la base de datos de back-end MDS con WSFC. Otras partes de MDS, como aplicaciones web y Administrador de configuración de MDS, se pueden ejecutar en el nodo de WSFC o fuera de WSFC, siempre y cuando MDS puede conectarse a la disponibilidad.

1.  Abra **Administrador de configuración de servicio de datos de Master** en un nodo, haga clic en **configuración de base de datos**y, a continuación, haga clic en **Create Database** para iniciar el **Asistente para crear la base de datos**.

2.  En el **servidor de base de datos** página, escriba el nombre DNS del agente de escucha AG en el **instancia de SQL Server** cuadro de texto, haga clic en **Probar conexión**y, a continuación, haga clic en **siguiente**. Consulte la figura 21.

    ![Configurar servidor de base de datos con el del agente de escucha](media/Fig21_MDSDatabaseServerListener.png)

    Figura 21

3.  En el **base de datos** página, escriba el nombre de la base de datos que creó en el [crear un grupo de disponibilidad](#create-an-availability-group) sección y, a continuación, haga clic en **siguiente**. Consulte la figura 22.

    ![Crear y configurar la base de datos](media/Fig22_MDSCreateDatabase.png)

    Figura 22

4.  Completar la **crear base de datos** **asistente**. Para obtener más información, consulte [instalación de servicios de datos maestra y configuración](https://docs.microsoft.com/sql/master-data-services/master-data-services-installation-and-configuration).

5.  Haga clic en **aplicaciones Web** en **Administrador de configuración de servicio de datos de Master** para configurar la aplicación Web y, a continuación, haga clic en **aplicar** para aplicar la configuración a MDS. Consulte la figura 23. Para obtener más información, consulte [instalación de servicios de datos maestra y configuración](https://docs.microsoft.com/sql/master-data-services/master-data-services-installation-and-configuration).

    ![Configurar la aplicación Web](media/Fig23_MDSWebApplication.png)

    Figura 23

    Se ha completado el programa de instalación MDS. Puede repetir los pasos anteriores para configurar MDS para ejecutar en todos los nodos. La base de datos back-end es el mismo en el mismo AG.

6.  Si ha creado una base de datos temporal (vea [crear un grupo de disponibilidad](#create-an-availability-group) sección) para crear AlwaysOn AG, a continuación, debe quitar la base de datos temporal

    Para obtener más información acerca de Master Data Services, consulte [Master Data Services](https://docs.microsoft.com/sql/master-data-services/master-data-services-overview-mds).

## <a name="conclusion"></a>Conclusión

En estas notas del producto, hemos visto cómo instalar y configurar la base de datos de back-end de Master Data Services encima de grupo de disponibilidad AlwaysOn de SQL Server. Esta configuración proporciona alta disponibilidad y recuperación ante desastres en la base de datos de back-end de Master Data Services. Para implementar esta configuración, es necesario instalar y configurar Windows Server conmutación por error de clúster, SQL Server grupo de disponibilidad AlwaysOn y Master Data Services.

## <a name="feedback"></a>Comentarios

¿Le ha resultado útil este documento? Envíenos sus comentarios, haga clic en **comentarios** en la parte superior del artículo. 

Sus comentarios nos ayudarán a mejorar la calidad de las notas del producto que publiquemos. 


