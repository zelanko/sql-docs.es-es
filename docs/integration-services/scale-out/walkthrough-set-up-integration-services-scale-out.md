---
title: "Tutorial: configuración de la escalabilidad horizontal de SQL Server Integration Services | Microsoft Docs"
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
ms.openlocfilehash: ec9744a1efb0e78aca55e85e7f9f3eca007de5a2
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="walkthrough-set-up-integration-services-scale-out"></a>Tutorial: configuración del escalado horizontal de Integration Services
Para configurar la escalabilidad horizontal de [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)], lleve a cabo las siguientes tareas. 

> [!NOTE]
> Si va a instalar la escalabilidad horizontal en un equipo, instale las características de patrón y trabajo de escalabilidad horizontal al mismo tiempo. Al hacerlo, el punto de conexión se genera automáticamente para conectarse a patrón de escalado horizontal. 

* [Instalar el patrón de escalado horizontal](#InstallMaster)

* [Instalar el trabajador de escalado horizontal](#InstallWorker)

* [Instalar el certificado de cliente del trabajador de escalado horizontal](#InstallCert)

* [Abrir el puerto del firewall](#Firewall)

* [Iniciar el servicio de patrón y trabajador de escalado horizontal de SQL Server](#Start)

* [Habilitar el patrón de escalado horizontal](#EnableMaster)

* [Habilitar el modo de autenticación de SQL Server](#EnableAuth)

* [Habilitar el trabajador de escalado horizontal](#EnableWorker)

## <a name="InstallMaster"></a> Instalar el patrón de escalado horizontal

Para habilitar la funcionalidad del patrón de escalabilidad horizontal, debe instalar los servicios del motor de base de datos, [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)] y su característica de patrón de escalabilidad horizontal cuando configure [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. 

Para obtener información sobre cómo configurar los servicios de motor de base de datos y [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)], consulte [Instalar el motor de base de datos de SQL Server](../../database-engine/install-windows/install-sql-server-database-engine.md) e [Instalar Integration Services](../install-windows/install-integration-services.md).
> [!NOTE]
> Para usar la cuenta de autenticación de SQL predeterminada para el registro de escalabilidad horizontal, seleccione Modo mixto para el modo de autenticación en la página Configuración del motor de base de datos durante su instalación. Consulte [Change the account for Scale Out logging](change-logdb-account.md) (Cambio de cuenta para el registro de la escalabilidad horizontal) para obtener más información.

**Para instalar la característica de patrón de escalado horizontal, use el Asistente para la instalación de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] o la línea de comandos.**

- Pasos del Asistente para la instalación de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]
  1.  En la página **Selección de características**, seleccione **Patrón de escalabilidad horizontal**, que aparece en [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].   
  ![Selección de características: Master](media/feature-select-master.PNG)
  
  2.  En la página **Configuración del servidor** , seleccione la cuenta para ejecutar el servicio **Patrón de escalado horizontal de SQL Server Integration Services** y, después, seleccione el **tipo de inicio**.  
  ![Configuración del servidor](media/server-config.PNG)
  3.  En la página **Configuración del patrón de escalado horizontal de Integration Services** , especifique el número de puerto que usa el patrón de escalado horizontal para comunicarse con el trabajador de escalado horizontal. El número de puerto predeterminado es 8391.  
  ![Configuración del patrón](media/master-config.PNG "Configuración del patrón")
  4.  Especifique el certificado SSL usado para proteger la comunicación entre el patrón y el trabajo de escalabilidad horizontal; para ello, siga uno de los siguientes pasos.
    * Deje que el proceso de instalación cree un certificado SSL autofirmado predeterminado; para ello, haga clic en **Crear un nuevo certificado SSL**.  El certificado predeterminado se instala en Entidades de certificación raíz de confianza, Equipo local. Puede especificar los CN en este certificado. El nombre de host del punto de conexión principal debe incluirse en los CN. De forma predeterminada, se incluyen el nombre de la máquina y la dirección IP del nodo principal.
    * Para seleccionar un certificado SSL existente del equipo local, haga clic en **Usar un certificado SSL existente** y en **Examinar**. La huella digital del certificado aparece en el cuadro de texto. Haga clic en **Examinar** para que se muestren los certificados almacenados en Entidades de certificación raíz de confianza, Equipo local. El certificado que vaya a seleccionar debe almacenarse aquí.       
![Configuración del patrón 2](media/master-config-2.PNG "Configuración del patrón 2")
  5.  Finalice el Asistente para la instalación de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].
- Pasos para la línea de comandos

    Siga las instrucciones descritas en [Instalar SQL Server desde el símbolo del sistema](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md). Establezca los parámetros relacionados del patrón de escalado horizontal siguiendo estos pasos.
  1.  Agregue IS_Master al parámetro /FEATURES.
  2.  Para configurar el patrón de escalabilidad horizontal, especifique los siguientes parámetros y sus valores: /ISMASTERSVCACCOUNT, /ISMASTERSVCPASSWORD, /ISMASTERSVCSTARTUPTYPE, /ISMASTERSVCPORT, /ISMasterSVCSSLCertCN (opcional), /ISMASTERSVCTHUMBPRINT (opcional).

> [!Note]
> Si el patrón de escalabilidad horizontal no está instalado junto con el motor de base de datos y este motor es una instancia con nombre, debe configurar SqlServerName en el archivo de configuración de servicio del patrón de escalabilidad horizontal después de la instalación. Vea [Scale Out Master](integration-services-ssis-scale-out-master.md) (Patrón de escalabilidad horizontal) para obtener más detalles.

## <a name="InstallWorker"></a> Instalar el trabajador de escalado horizontal
 
Para habilitar la funcionalidad de trabajador de escalado horizontal, debe instalar [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)] y la característica de trabajador de escalado horizontal en el programa de instalación de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].

**Para instalar la característica de trabajador de escalado horizontal, use el Asistente para la instalación de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] o la línea de comandos.**

- Pasos del Asistente para la instalación de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]
  1.  En la página **Selección de características**, seleccione **Trabajo de escalabilidad horizontal**, que aparece en [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].   
  ![Selección de características: Worker](media/feature-select-worker.PNG)
  2. En la página **Configuración del servidor** , seleccione la cuenta para ejecutar el servicio **Trabajador de escalado horizontal de SQL Server Integration Services** y, después, seleccione el **tipo de inicio**.    
  ![Configuración del servidor 2](media/server-config-2.PNG "Configuración del servidor 2")
  3. En la página **Configuración del trabajador de escalado horizontal de Integration Services** , especifique el punto de conexión para conectarse al patrón de escalado horizontal. 
      > [!Note]
      > Puede omitir la configuración del nodo de trabajo (pasos 3 y 4) aquí y asociar el trabajo con el patrón de escalabilidad horizontal con el [administrador de escalabilidad horizontal](integration-services-ssis-scale-out-manager.md) después de la instalación.

    - Para un entorno de **un solo equipo**, el punto de conexión se genera automáticamente al instalar simultáneamente el patrón y el trabajo de escalabilidad horizontal. 
    - Para un entorno de **varios equipos**, el punto de conexión está formado por el nombre o la dirección IP del equipo que tiene instalado el patrón de escalabilidad horizontal y el número de puerto especificado durante la instalación del patrón de escalabilidad horizontal.    
   ![Configuración del trabajo 1](media/worker-config.PNG "Configuración del trabajo 1")    

  4. Para un entorno de **varios equipos**, especifique el certificado SSL de cliente usado para validar el patrón de escalabilidad horizontal. Para un entorno de **un solo equipo**, no es necesario especificar el certificado SSL de cliente. 
  
     > [!NOTE]
     > Si el certificado SSL que usa el patrón de escalabilidad horizontal está autofirmado, debe haber un certificado SSL de cliente correspondiente instalado en el equipo que contiene el trabajo de escalabilidad horizontal. Si proporciona la ruta de acceso del archivo del certificado SSL de cliente en la página **Configuración del trabajo de escalabilidad horizontal de Integration Services**, se instalará automáticamente; en caso contrario, tendrá que instalar el certificado manualmente más adelante. 
     
     Haga clic en **Examinar** para buscar el archivo de certificado (*.cer). Para usar el certificado SSL predeterminado, seleccione el archivo SSISScaleOutMaster.cer, ubicado en \<unidad\>:\Archivos de programa\Microsoft SQL Server\140\DTS\Binn en el equipo en el que se ha instalado el patrón de escalabilidad horizontal.   
   ![Configuración de trabajo 2](media/worker-config-2.PNG "Configuración de trabajo 2")
  5. Finalice el Asistente para la instalación de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].
- Pasos para la línea de comandos

    Siga las instrucciones descritas en [Instalar SQL Server desde el símbolo del sistema](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md). Establezca los parámetros relacionados del trabajador de escalado horizontal siguiendo estos pasos.
    1.  Agregue IS_Worker al parámetro /FEATURES.
    2. Para configurar el trabajo de escalabilidad horizontal, especifique los siguientes parámetros y sus valores: /ISWORKERSVCACCOUNT, /ISWORKERSVCPASSWORD, /ISWORKERSVCSTARTUPTYPE, /ISWORKERSVCMASTER (opcional), /ISWORKERSVCCERT (opcional).

 
## <a name="InstallCert"></a> Instalar el certificado de cliente del trabajador de escalado horizontal

Durante la instalación del trabajo de escalabilidad horizontal, se creará e instalará automáticamente un certificado de trabajo en el equipo. También se instalará un certificado de cliente correspondiente, SSISScaleOutWorker.cer, en \<unidad\>:\Archivos de programa\Microsoft SQL Server\140\DTS\Binn. Para que el patrón de escalabilidad horizontal autentique el trabajo de escalabilidad horizontal, debe agregar este certificado de cliente al almacén raíz del equipo local con el patrón de escalabilidad horizontal.
  
Para agregar el certificado de cliente al almacén raíz, haga doble clic en el archivo .cer y, luego, haga clic en **Instalar certificado** en el cuadro de diálogo del certificado. Se abre el **Asistente para importar certificados** .  

## <a name="Firewall"></a> Abrir el puerto del firewall

Abra el puerto especificado durante la instalación del patrón de escalabilidad horizontal y el puerto de SQL Server (1433 de manera predeterminada) usando Firewall de Windows en el equipo del patrón de escalabilidad horizontal.
    
## <a name="Start"></a> Iniciar los servicios de patrón y trabajador de escalado horizontal de SQL Server

Si el tipo de inicio de los servicios no se establece en Automático durante la instalación, inicie los servicios de patrón de escalabilidad horizontal de SQL Server Integration Services 14.0 (SSISScaleOutMaster140) y trabajo de escalabilidad horizontal de SQL Server Integration Services 14.0 (SSISScaleOutWorker140). 

> [!Note]
> Después de abrir el puerto del firewall, también debe reiniciar el servicio de trabajo de escalabilidad horizontal.
   
## <a name="EnableMaster"></a> Habilitar el patrón de escalado horizontal

Haga clic en **Habilitar este servidor como patrón de escalado horizontal de SSIS** en el cuadro de diálogo **Crear catálogo** al crear el catálogo de SSISDB en [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio_md](../../includes/ssmanstudio-md.md)]. Como alternativa, se puede habilitar el patrón de escalabilidad horizontal con el [administrador de escalabilidad horizontal](integration-services-ssis-scale-out-manager.md) después de crear el catálogo.

## <a name="EnableAuth"></a> Habilitar el modo de autenticación de SQL Server
Si la autenticación de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] no está habilitada durante la instalación del motor de base de datos, habilite el modo de autenticación de SQL Server en la instancia de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] que hospeda el catálogo de SSISDB. 

La ejecución de paquetes no se bloquea si la autenticación de SQL Server está deshabilitada, aunque el registro de ejecución no podrá escribir en SSISDB.

## <a name="EnableWorker"></a> Habilitar el trabajador de escalado horizontal

El trabajo de escalabilidad horizontal puede habilitarse con el [administrador de escalabilidad horizontal](integration-services-ssis-scale-out-manager.md), que proporciona una interfaz gráfica de usuario, o habilitarse con el procedimiento almacenado que verá a continuación.

Para habilitar el trabajador de escalado horizontal, ejecute el procedimiento almacenado *[catalog].[enable_worker_agent]* con **WorkerAgentId** como parámetro. 

Obtendrá el valor **WorkerAgentId** de la vista de base de datos *[catalog].[worker_agents]* en SSISDB, después de que el trabajador de escalado horizontal se haya registrado en el patrón de escalado horizontal. El registro tarda varios minutos una vez iniciados los servicios de patrón y trabajador de escalado horizontal.

#### <a name="example"></a>Ejemplo
En este ejemplo se habilita el trabajo de escalabilidad horizontal en el equipo computerA.
```sql
SELECT WorkerAgentId, MachineName FROM [catalog].[worker_agents]
GO
-- Result: --
-- WorkerAgentId                           MachineName  --
-- 6583054A-E915-4C2A-80E4-C765E79EF61D    computerA    --

EXEC [catalog].[enable_worker_agent] '6583054A-E915-4C2A-80E4-C765E79EF61D'
GO 
```
## <a name="next-steps"></a>Pasos siguientes
Ha finalizado la configuración de la característica de escalado horizontal. Ahora puede ejecutar paquetes en escalabilidad horizontal. Para obtener más información, consulte [Execute Packages in Integration Services (SSIS) Scale Out](run-packages-in-integration-services-ssis-scale-out.md) (Ejecutar paquetes en el escalado horizontal de Integration Services (SSIS)).
