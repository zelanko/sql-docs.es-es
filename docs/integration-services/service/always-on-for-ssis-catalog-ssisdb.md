---
title: "Always On for SSIS Catalog (SSISDB) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.ssis.ssms.alwayson.f1"
ms.assetid: 7f089455-35ee-4c13-884e-9254b685d07d
caps.latest.revision: 17
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 16
---
# Always On for SSIS Catalog (SSISDB)
  La característica Grupos de disponibilidad AlwaysOn es una solución de alta disponibilidad y de recuperación ante desastres que proporciona una alternativa empresarial a la creación de reflejo de la base de datos. Un grupo de disponibilidad admite un entorno de conmutación por error para un conjunto discreto de bases de datos de usuario, conocido como “bases de datos de disponibilidad”, que realizan la conmutación por error conjuntamente. Para obtener más información, vea [Grupos de disponibilidad AlwaysOn](https://msdn.microsoft.com/library/hh510230.aspx).  
  
 Con el objetivo de ofrecer alta disponibilidad al catálogo de SSIS (SSISDB) y su contenido (proyectos, paquetes, registros de ejecución, etc.), puede agregar la base de datos SSISDB (al igual que cualquier otra base de datos de usuario) a un grupo de disponibilidad AlwaysOn. Cuando se produce una conmutación por error, uno de los nodos secundarios se convierte automáticamente en el nuevo nodo principal.  
 
 > [!IMPORTANT]  Cuando se produce una conmutación por error, los paquetes que se estuvieran ejecutando no se reinician o reanudan. 
 
 **En este tema:**  
  
1.  [Requisitos previos](../../integration-services/service/always-on-for-ssis-catalog-ssisdb.md#prereq)  
  
2.  [Configuración de la compatibilidad con SSIS para AlwaysOn](../../integration-services/service/always-on-for-ssis-catalog-ssisdb.md#Firsttime)  
  
3.  [Actualización de SSISDB en un grupo de disponibilidad](../../integration-services/service/always-on-for-ssis-catalog-ssisdb.md#Upgrade)  
  
##  <a name="a-nameprereqa-prerequisites"></a><a name="prereq"></a> Requisitos previos  
 Debe llevar a cabo los siguientes pasos, que constituyen unos requisitos previos, antes de habilitar la compatibilidad de AlwaysOn para la base de datos SSISDB.  
  
1.  Configure un clúster de conmutación por error de Windows. Consulte la entrada de blog [Installing the Failover Cluster Feature and Tools for Windows Server 2012](http://blogs.msdn.com/b/clustering/archive/2012/04/06/10291601.aspx) (Instalación de las herramientas y la característica de clúster de conmutación por error para Windows Server 2012) a fin de obtener instrucciones. Debe instalar la característica y las herramientas en todos los nodos del clúster.  
  
2.  Instale SQL Server 2016 con la característica Integration Services (SSIS) en cada nodo del clúster.  
  
3.  Habilite la característica AlwaysOn para cada instancia de SQL Server. Consulte [Habilitar y deshabilitar grupos de disponibilidad AlwaysOn (SQL Server)](https://msdn.microsoft.com/library/ff878259.aspx) para obtener más información.  
  
##  <a name="a-namefirsttimea-configure-ssis-support-for-always-on"></a><a name="Firsttime"></a> Configuración de la compatibilidad con SSIS para AlwaysOn  
  
-   [Paso 1: creación del catálogo de Integration Services](../../integration-services/service/always-on-for-ssis-catalog-ssisdb.md#Step1)  
  
-   [Paso 2: adición de SSISDB a un grupo de disponibilidad AlwaysOn](../../integration-services/service/always-on-for-ssis-catalog-ssisdb.md#Step2)  
  
-   [Paso 3: habilitación de la compatibilidad con SSIS para AlwaysOn](../../integration-services/service/always-on-for-ssis-catalog-ssisdb.md#Step3)  
  
> [!IMPORTANT]  
>  -   Debe realizar estos pasos en el **nodo principal** del grupo de disponibilidad.  
> -   Debe habilitar la **compatibilidad con SSIS para AlwaysOn** después de agregar SSISDB a un grupo AlwaysOn.  
  
###  <a name="a-namestep1a-step-1-create-integration-services-catalog"></a><a name="Step1"></a>Paso 1: creación del catálogo de Integration Services  
  
1.  Inicie **SQL Server Management Studio** y conéctese a una instancia de SQL Server en el clúster que quiere establecer como el **nodo principal** del grupo de alta disponibilidad AlwaysOn para SSISDB.  
  
2.  En el Explorador de objetos, expanda el nodo del servidor, haga clic con el botón derecho en el nodo **Catálogos de Integration Services** y, después, haga clic en **Crear catálogo**.  
  
3.  Haga clic en **Habilitar integración con CLR**. El catálogo usar los procedimientos almacenados de CLR.  
  
4.  Haga clic en **Habilitar la ejecución automática del procedimiento almacenado de Integration Services al iniciar SQL Server** para permitir que el procedimiento almacenado [catalog.startup](https://msdn.microsoft.com/library/hh230984.aspx) se ejecute cada vez que se reinicie la instancia del servidor de SSIS. El procedimiento almacenado realiza el mantenimiento del estado de las operaciones del catálogo de SSISDB. Corrige el estado de los paquetes que estaban en ejecución si y cuando la instancia del servidor de SSIS se bloquea.  
  
5.  Escriba una **contraseña**y haga clic en **Aceptar**. La contraseña protege la clave maestra de la base de datos que se usar para cifrar los datos del catálogo. Guarde la contraseña en un lugar seguro. Se recomienda que haga también una copia de seguridad de la clave maestra de la base de datos. Para más información, consulte [Back Up a Database Master Key](https://msdn.microsoft.com/library/aa337546.aspx).  
  
###  <a name="a-namestep2a-step-2-add-ssisdb-to-an-always-on-availability-group"></a><a name="Step2"></a> Paso 2: adición de SSISDB a un grupo de disponibilidad AlwaysOn  
 Puede agregar la base de datos SSISDB a un grupo de disponibilidad AlwaysOn prácticamente con el mismo procedimiento que emplearía para agregar cualquier otra base de datos de usuario a un grupo de disponibilidad. Consulte [Usar el Asistente para grupo de disponibilidad (SQL Server Management Studio)](https://msdn.microsoft.com/library/hh403415.aspx).  
  
 Debe escribir la contraseña que especificó al crear el catálogo de SSIS en la página **Seleccionar bases de datos** del **Asistente para nuevo grupo de disponibilidad** .  
  
 ![New Availability Group](../../integration-services/service/media/ssis-newavailabilitygroup.png "New Availability Group")  
  
###  <a name="a-namestep3a-step-3-enable-ssis-support-for-always-on"></a><a name="Step3"></a> Paso 3: habilitación de la compatibilidad con SSIS para AlwaysOn  
 Después de crear el catálogo de Integration Services, haga clic con el botón derecho en el nodo **Catálogos de Integration Services** y haga clic en **Enable AlwaysOn Support**(Habilitar compatibilidad con AlwaysOn). Verá el siguiente cuadro de diálogo: **Habilitar compatibilidad con AlwaysOn** . Si este elemento de menú está deshabilitado, confirme que tiene todos los requisitos previos instalados y haga clic en **Actualizar**.  
  
 ![Enable Support for AlwaysOn](../../integration-services/service/media/ssis-enablesupportforalwayson.png "Enable Support for AlwaysOn")  
  
> [!WARNING]  
>  No se admite la conmutación por error automática de la base de datos SSISDB hasta que habilite la compatibilidad con SSIS para AlwaysOn.  
  
 Las réplicas secundarias recién agregadas desde el grupo de disponibilidad AlwaysOn se mostrarán en la tabla. Haga clic en **Conectar** de cada réplica de la lista y escriba las credenciales de autenticación para conectarse a ella. La cuenta de usuario debe ser miembro del grupo sysadmin en cada réplica para habilitar la compatibilidad con SSIS para AlwaysOn. Después de conectarse correctamente a cada réplica, haga clic en **Aceptar** a fin de habilitar la compatibilidad con SSIS para AlwaysOn.  
  
##  <a name="a-nameupgradea-upgrading-ssisdb-in-an-availability-group"></a><a name="Upgrade"></a> Actualización de SSISDB en un grupo de disponibilidad  
 Si va a actualizar SQL Server desde una versión anterior y SSISDB se encuentra en un grupo de disponibilidad AlwaysOn, la regla "Comprobación de SSISDB en grupo de disponibilidad AlwaysOn" podría bloquear la actualización. Este bloqueo se produce porque la actualización se ejecuta en modo de usuario único, mientras que una base de datos de disponibilidad debe ser multiusuario. Por lo tanto, durante la actualización o la aplicación de una revisión, todas las bases de datos disponibilidad, incluida SSISDB, se desconectan y no se actualizan ni se les aplica la revisión. Para permitir que actualización continúe, tendrá que quitar SSISDB primero del grupo de disponibilidad; después, actualizar cada una o aplicarle una revisión y, por último, volver a agregar SSISDB al grupo de disponibilidad.  
  
 Si la regla "Comprobación de SSISDB en grupo de disponibilidad AlwaysOn" está causando un bloqueo, tendrá que seguir estos pasos para actualizar SQL Server.  
  
1.  Quite la base de datos SSISDB del grupo de disponibilidad. Para obtener más información, vea [Quitar una base de datos secundaria de un grupo de disponibilidad &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/remove-a-secondary-database-from-an-availability-group-sql-server.md) y [Quitar una base de datos principal de un grupo de disponibilidad &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/remove-a-primary-database-from-an-availability-group-sql-server.md).  
  
2.  Haga clic en **Volver a ejecutar** en el Asistente para actualización. Se aplicará la regla "Comprobación de SSISDB en grupo de disponibilidad AlwaysOn".  
  
3.  Haga clic en **Siguiente** para continuar con la actualización.  
  
4.  Después de actualizar todos los nodos, vuelva a agregar la base de datos SSISDB al grupo de disponibilidad AlwaysOn. Para obtener más información, vea [Agregar una base de datos a un grupo de disponibilidad &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/add-a-database-to-an-availability-group-sql-server.md).  
  
 Si no se encuentra con un bloqueo al actualizar SQL Server y SSISDB está en un grupo de disponibilidad AlwaysOn, tendrá que actualizar SSISDB por separado tras actualizar el motor de base de datos de SQL Server. Use el Asistente para actualización de SQL Server Integration Services a fin de actualizar SSISDB como se describe en el siguiente procedimiento.  
  
1.  Saque la base de datos SSISDB del grupo de disponibilidad o elimine el grupo de disponibilidad, si SSISDB es la única base de datos de este. Tendrá que iniciar **SQL Server Management Studio** en el **nodo principal** del grupo de disponibilidad para realizar esta tarea.  
  
2.  Quite la base de datos SSISDB de todos los **nodos de réplicas**.  
  
3.  Actualice la base de datos SSISDB en el **nodo principal**. En el**Explorador de objetos** de SQL Server Management Studio, expanda **Catálogos de Integration Services**, haga clic con el botón derecho en **SSISDB**y, después, seleccione **Actualización de base de datos**. Siga las instrucciones del **Asistente para actualización de SSISDB** a fin de actualizar la base de datos. Tendrá que iniciar el **Asistente para actualización de SSIDB** localmente en el **nodo primario**.  
  
4.  Siga las instrucciones de [Paso 2: adición de SSISDB a un grupo de disponibilidad AlwaysOn](../../integration-services/service/always-on-for-ssis-catalog-ssisdb.md#Step2) para volver a agregar SSISDB a un grupo de disponibilidad.  
  
5.  Siga las instrucciones de [Paso 3: habilitación de la compatibilidad con SSIS para AlwaysOn](../../integration-services/service/always-on-for-ssis-catalog-ssisdb.md#Step3).  
  
  