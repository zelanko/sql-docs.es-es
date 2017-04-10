---
title: "Tutorial: configuraci&#243;n del escalado horizontal de Integration Services | Microsoft Docs"
ms.custom: ""
ms.date: "01/18/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: cabb78a2-f234-46c3-842d-53aa2df8dfb3
caps.latest.revision: 10
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 7
---
# Tutorial: configuraci&#243;n del escalado horizontal de Integration Services

Puede configurar [!INCLUDE[ssISnoversion_md](../includes/ssisnoversion-md.md)] el escalado horizontal llevando a cabo las siguientes tareas. 

> [!NOTE] Si va a instalar el escalado horizontal en un equipo, se recomienda que instale las características patrón y trabajador de escalado horizontal al mismo tiempo. Al hacerlo, el punto de conexión se genera automáticamente para conectarse a patrón de escalado horizontal. 

* [Instalar el patrón de escalado horizontal](#InstallMaster)

* [Instalar el trabajador de escalado horizontal](#InstallWorker)

* [Instalar el certificado de cliente del trabajador de escalado horizontal](#InstallCert)

* [Abrir el puerto del firewall](#Firewall)

* [Iniciar el servicio de patrón y trabajador de escalado horizontal de SQL Server](#Start)

* [Habilitar el patrón de escalado horizontal](#EnableMaster)

* [Habilitar el modo de autenticación de SQL Server](#EnableAuth)

* [Habilitar el trabajador de escalado horizontal](#EnableWorker)

## <a name="a-nameinstallmastera-install-scale-out-master"></a><a name="InstallMaster"></a> Instalar el patrón de escalado horizontal

Para habilitar la funcionalidad del patrón de escalado horizontal, debe instalar los servicios del motor de base de datos, [!INCLUDE[ssISnoversion_md](../includes/ssisnoversion-md.md)] y su característica de patrón de escalado horizontal cuando configure [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)]. 

Para obtener información sobre cómo configurar los servicios de motor de base de datos y [!INCLUDE[ssISnoversion_md](../includes/ssisnoversion-md.md)], consulte [Instalar el motor de base de datos de SQL Server](../database-engine/install-windows/install-sql-server-database-engine.md) e [Instalar Integration Services](../integration-services/install-windows/install-integration-services.md).
> [!NOTE]
> Durante la instalación del motor de base de datos, seleccione Modo mixto para el modo de autenticación en la página Configuración del motor de base de datos. 

**Para instalar la característica de patrón de escalado horizontal, use el Asistente para la instalación de [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] o la línea de comandos.**

- Pasos del Asistente para la instalación de [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)]
  1.  En la página **Selección de características**, seleccione **Patrón de escalado horizontal**, que aparece en [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].   
  ![Selección de características: Master](../integration-services/media/feature-select-master.PNG)
  
  2.  En la página **Configuración del servidor**, seleccione la cuenta para ejecutar el servicio **Patrón de escalado horizontal de SQL Server Integration Services** y, después, seleccione el **tipo de inicio**.  
  ![Configuración del servidor](../integration-services/media/server-config.PNG)
  3.  En la página **Configuración del patrón de escalado horizontal de Integration Services**, especifique el número de puerto que usa el patrón de escalado horizontal para comunicarse con el trabajador de escalado horizontal. El número de puerto predeterminado es 8391.  
  ![Master Config](../integration-services/media/master-config.PNG "Master Config")
  4.  Especifique el certificado SSL usado para proteger la comunicación entre el patrón y el trabajador de escalado horizontal; para ello, siga uno de los siguientes pasos.
    * Deje que el proceso de instalación cree un certificado SSL autofirmado predeterminado; para ello, haga clic en **Crear un nuevo certificado SSL**. El certificado predeterminado se instala en Entidades de certificación raíz de confianza, Equipo local.
    * Seleccione un certificado SSL existente del equipo local; para ello, haga clic en **Usar un certificado SSL existente** y en **Examinar**. La huella digital del certificado aparece en el cuadro de texto. Haga clic en **Examinar** para que se muestren los certificados almacenados en Entidades de certificación raíz de confianza, Equipo local. El certificado que vaya a seleccionar debe almacenarse aquí.       
![Master Config 2](../integration-services/media/master-config-2.PNG "Master Config 2")
  5.  Finalice el Asistente para la instalación de [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)].
- Pasos para la línea de comandos

    Siga las instrucciones descritas en [Instalar SQL Server desde el símbolo del sistema](../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md). Establezca los parámetros relacionados del patrón de escalado horizontal siguiendo estos pasos.
  1.  Agregue IS_Master al parámetro /FEATURES.
  2.  Configure el patrón de escalado horizontal con los siguientes parámetros: /ISMASTERSVCACCOUNT, /ISMASTERSVCPASSWORD, /ISMASTERSVCSTARTUPTYPE, /ISMASTERSVCPORT e /ISMASTERSVCTHUMBPRINT(opcional).
  
## <a name="a-nameinstallworkera-install-scale-out-worker"></a><a name="InstallWorker"></a> Instalar el trabajador de escalado horizontal
 
Para habilitar la funcionalidad de trabajador de escalado horizontal, debe instalar [!INCLUDE[ssISnoversion_md](../includes/ssisnoversion-md.md)] y la característica de trabajador de escalado horizontal en el programa de instalación de [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)].

**Para instalar la característica de trabajador de escalado horizontal, use el Asistente para la instalación de [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] o la línea de comandos.**

- Pasos del Asistente para la instalación de [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)]
  1.  En la página **Selección de características**, seleccione **Trabajador de escalado horizontal**, que aparece en [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].   
  ![Selección de características: Worker](../integration-services/media/feature-select-worker.PNG)
  2. En la página **Configuración del servidor**, seleccione la cuenta para ejecutar el servicio **Trabajador de escalado horizontal de SQL Server Integration Services** y, después, seleccione el **tipo de inicio**.    
  ![Server Config 2](../integration-services/media/server-config-2.PNG "Server Config 2")
  3. En la página **Configuración del trabajador de escalado horizontal de Integration Services**, especifique el punto de conexión para conectarse al patrón de escalado horizontal. 
    - Para un entorno de **un solo equipo**, el punto de conexión se genera automáticamente al instalar simultáneamente el patrón y el trabajador de escalado horizontal. 
    - Para un entorno de **varios equipos**, el punto de conexión está formado por el nombre o la dirección IP del equipo que tiene instalado el patrón de escalado horizontal y el número de puerto especificado durante la instalación del patrón de escalado horizontal.    
   ![Worker Config 1](../integration-services/media/worker-config-1.PNG "Worker Config 1")
    
  4. Para un entorno de **varios equipos**, especifique el certificado SSL de cliente usado para validar el patrón de escalado horizontal. Para un entorno de **un solo equipo**, no es necesario especificar el certificado SSL de cliente. 
  
     > [!NOTE] Si el certificado SSL usado por el patrón de escalado horizontal está autofirmado, debe haber un certificado SSL de cliente correspondiente instalado en el equipo que contiene el trabajador de escalado horizontal. Si proporciona la ruta de acceso del archivo del certificado SSL de cliente en la página **Configuración del trabajador de escalado horizontal de Integration Services**, se instalará automáticamente; en caso contrario, tendrá que instalar el certificado manualmente más adelante. 
     
     Haga clic en **Examinar** para buscar el archivo de certificado (*.cer). Para usar el certificado SSL predeterminado, seleccione el archivo SSISScaleOutMaster.cer, ubicado en \<unidad\>:\Archivos de programa\Microsoft SQL Server\140\DTS\Binn, del equipo en el que se ha instalado el patrón de escalado horizontal.   
   ![Worker Config 2](../integration-services/media/worker-config-2.PNG "Worker Config 2")
  5. Finalice el Asistente para la instalación de [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)].
- Pasos para la línea de comandos

    Siga las instrucciones descritas en [Instalar SQL Server desde el símbolo del sistema](../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md). Establezca los parámetros relacionados del trabajador de escalado horizontal siguiendo estos pasos.
    1.  Agregue IS_Worker al parámetro /FEATURES.
    2. Configure el trabajador de escalado horizontal con los siguientes parámetros: /ISWORKERSVCACCOUNT, /ISWORKERSVCPASSWORD, /ISWORKERSVCSTARTUPTYPE, /ISWORKERSVCMASTER (opcional) e /ISWORKERSVCCERT(opcional).

 
## <a name="a-nameinstallcerta-install-scale-out-worker-client-certificate"></a><a name="InstallCert"><a/> Instalar el certificado de cliente del trabajador de escalado horizontal

Durante la instalación del trabajador de escalado horizontal se creará e instalará automáticamente un certificado del trabajador en el equipo. También se instalará un certificado de cliente correspondiente, SSISScaleOutWorker.cer, en \<unidad\>:\Archivos de programa\Microsoft SQL Server\140\DTS\Binn. Para que el patrón de escalado horizontal autentique el trabajador de escalado horizontal, debe agregar este certificado de cliente al almacén raíz del equipo local con el patrón de escalado horizontal.
  
Para agregar el certificado de cliente al almacén raíz, haga doble clic en el archivo .cer y, luego, haga clic en **Instalar certificado** en el cuadro de diálogo del certificado. Se abre el **Asistente para importar certificados**.  

## <a name="a-namefirewalla-open-firewall-port"></a><a name="Firewall"><a/> Abrir el puerto del firewall

Abra el puerto especificado durante la instalación del patrón de escalado horizontal usando Firewall de Windows en el equipo que ejecuta el patrón de escalado horizontal.
    
## <a name="a-namestarta-start-sql-server-scale-out-master-and-worker-services"></a><a name="Start"></a> Iniciar los servicios de patrón y trabajador de escalado horizontal de SQL Server

Si el tipo de inicio de los servicios no se establece en Automático durante la instalación anterior, inicie los servicios de patrón de escalado horizontal de SQL Server Integration Services 14.0 (SSISScaleOutMaster140) y trabajador de escalado horizontal de SQL Server Integration Services 14.0 (SSISScaleOutWorker140). 

> [!NOTE]
>Después de abrir el puerto del firewall, debe reiniciar el servicio de trabajador de escalado horizontal.
   
## <a name="a-nameenablemastera-enable-scale-out-master"></a><a name="EnableMaster"></a> Habilitar el patrón de escalado horizontal

Haga clic en **Habilitar este servidor como patrón de escalado horizontal de SSIS** en el cuadro de diálogo **Crear catálogo** al crear el catálogo de SSISDB en [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio_md](../includes/ssmanstudio-md.md)].

## <a name="a-nameenableautha-enable-sql-server-authentication-mode"></a><a name="EnableAuth"></a> Habilitar el modo de autenticación de SQL Server
Si la autenticación de [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] no está habilitada durante la instalación del motor de base de datos, habilite el modo de autenticación de SQL Server en la instancia de [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] que hospeda el catálogo de SSISDB. 

La ejecución de paquetes no se bloquea si la autenticación de SQL Server está deshabilitada, aunque el registro de ejecución no podrá escribir en SSISDB.

## <a name="a-nameenableworkera-enable-scale-out-worker"></a><a name="EnableWorker"></a> Habilitar el trabajador de escalado horizontal
Para habilitar el trabajador de escalado horizontal, ejecute el procedimiento almacenado *[catalog].[enable_worker_agent]* con **WorkerAgentId** como parámetro. 

Obtendrá el valor **WorkerAgentId** de la vista de base de datos *[catalog].[worker_agents]* en SSISDB, después de que el trabajador de escalado horizontal se haya registrado en el patrón de escalado horizontal. El registro tarda varios minutos una vez iniciados los servicios de patrón y trabajador de escalado horizontal.

### <a name="example"></a>Ejemplo
En este ejemplo se habilita el trabajador de escalado horizontal en el equipo MachineA.
```tsql
SELECT WorkerAgentId, MachineName FROM [catalog].[worker_agents]
GO
-- Result: --
-- WorkerAgentId                           MachineName --
-- 6583054A-E915-4C2A-80E4-C765E79EF61D    MachineA    --

EXEC [catalog].[enable_worker_agent] '6583054A-E915-4C2A-80E4-C765E79EF61D'
GO 
```
## <a name="next-steps"></a>Pasos siguientes
Ha finalizado la configuración de la característica de escalado horizontal. Ahora puede ejecutar paquetes en el escalado horizontal. Para obtener más información, consulte [Execute Packages in Integration Services (SSIS) Scale Out](../integration-services/run-packages-in-integration-services-ssis-scale-out.md) (Ejecutar paquetes en el escalado horizontal de Integration Services (SSIS)).

