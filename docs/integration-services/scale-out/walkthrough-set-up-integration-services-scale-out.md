---
title: 'Tutorial: Configurar SQL Server Integration Services escalada | Documentos de Microsoft'
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
ms.openlocfilehash: 9cc5c653fe454b45148583f2e17654657a85b0a5
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="walkthrough-set-up-integration-services-scale-out"></a>Tutorial: configuración del escalado horizontal de Integration Services
Configurar [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)] horizontalmente realizando las siguientes tareas. 

> [!NOTE]
> Si va a instalar horizontalmente en un equipo, instale las características de escala Out maestra y de escala Out trabajo al mismo tiempo. Al hacerlo, el punto de conexión se genera automáticamente para conectarse a patrón de escalado horizontal. 

* [Instalar el patrón de escalado horizontal](#InstallMaster)

* [Instalar el trabajador de escalado horizontal](#InstallWorker)

* [Instalar el certificado de cliente del trabajador de escalado horizontal](#InstallCert)

* [Abrir el puerto del firewall](#Firewall)

* [Iniciar el servicio de patrón y trabajador de escalado horizontal de SQL Server](#Start)

* [Habilitar el patrón de escalado horizontal](#EnableMaster)

* [Habilitar el modo de autenticación de SQL Server](#EnableAuth)

* [Habilitar el trabajador de escalado horizontal](#EnableWorker)

## <a name="InstallMaster"></a> Instalar el patrón de escalado horizontal

Para habilitar la funcionalidad de escala Out maestro, debe instalar servicios del motor de base de datos, [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)]y su característica de escala Out maestra al configurar [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. 

Para obtener información sobre cómo configurar los servicios de motor de base de datos y [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)], consulte [Instalar el motor de base de datos de SQL Server](../../database-engine/install-windows/install-sql-server-database-engine.md) e [Instalar Integration Services](../install-windows/install-integration-services.md).
> [!NOTE]
> Para usar la cuenta de autenticación de SQL predeterminada para horizontalmente el registro, seleccione el modo mixto en el modo de autenticación en la página de configuración del motor de base de datos durante la instalación del motor de base de datos. Vea [cambiar la cuenta para el registro horizontalmente](change-logdb-account.md) para obtener más información.

**Para instalar la característica de patrón de escalado horizontal, use el Asistente para la instalación de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] o la línea de comandos.**

- Pasos del Asistente para la instalación de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]
  1.  En el **selección de características** página, seleccione **escala Out Master**, que aparece en [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].   
  ![Selección de características: Master](media/feature-select-master.PNG)
  
  2.  En la página **Configuración del servidor** , seleccione la cuenta para ejecutar el servicio **Patrón de escalado horizontal de SQL Server Integration Services** y, después, seleccione el **tipo de inicio**.  
  ![Configuración del servidor](media/server-config.PNG)
  3.  En la página **Configuración del patrón de escalado horizontal de Integration Services** , especifique el número de puerto que usa el patrón de escalado horizontal para comunicarse con el trabajador de escalado horizontal. El número de puerto predeterminado es 8391.  
  ![Configuración de master](media/master-config.PNG "configuración maestra")
  4.  Especifique el certificado SSL usado para proteger la comunicación entre escala Out maestra y de escala Out trabajo llevando a cabo una de las siguientes acciones.
    * Deje que el proceso de instalación cree un valor predeterminado, el certificado SSL autofirmado haciendo clic en **crear un nuevo certificado SSL**.  El certificado predeterminado se instala en Entidades de certificación raíz de confianza, Equipo local. Puede especificar el CNs en este certificado. El nombre de host del punto de conexión principal debe incluirse en CNs. De forma predeterminada, se incluyen el nombre del equipo y la dirección ip del nodo principal.
    * Seleccione una existente al SSL en el equipo local, haga clic en **usar un certificado SSL existente** y, a continuación, haga clic en **examinar** para seleccionar un certificado. La huella digital del certificado aparece en el cuadro de texto. Haga clic en **Examinar** para que se muestren los certificados almacenados en Entidades de certificación raíz de confianza, Equipo local. El certificado que vaya a seleccionar debe almacenarse aquí.       
![Configuración de master 2](media/master-config-2.PNG "Master configuración 2")
  5.  Finalice el Asistente para la instalación de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].
- Pasos para la línea de comandos

    Siga las instrucciones descritas en [Instalar SQL Server desde el símbolo del sistema](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md). Establezca los parámetros relacionados del patrón de escalado horizontal siguiendo estos pasos.
  1.  Agregue IS_Master al parámetro /FEATURES.
  2.  Configurar escala Out maestro mediante la especificación de los siguientes parámetros y sus valores: /ISMASTERSVCACCOUNT, /ISMASTERSVCPASSWORD, /ISMASTERSVCSTARTUPTYPE, /ISMASTERSVCPORT, /ISMasterSVCSSLCertCN(optional), /ISMASTERSVCTHUMBPRINT(optional).

> [!Note]
> Si escala Out maestra no está instalado junto con el motor de base de datos y el motor de base de datos es una instancia con nombre, debe configurar SqlServerName en el archivo de configuración de servicio de escala Out Master después de la instalación. Vea [escala Out Master](integration-services-ssis-scale-out-master.md) para obtener más información.

## <a name="InstallWorker"></a> Instalar el trabajador de escalado horizontal
 
Para habilitar la funcionalidad de trabajador de escalado horizontal, debe instalar [!INCLUDE[ssISnoversion_md](../../includes/ssisnoversion-md.md)] y la característica de trabajador de escalado horizontal en el programa de instalación de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].

**Para instalar la característica de trabajador de escalado horizontal, use el Asistente para la instalación de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] o la línea de comandos.**

- Pasos del Asistente para la instalación de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]
  1.  En el **selección de características** página, seleccione **escala Out trabajo**, que aparece en [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].   
  ![Selección de características: Worker](media/feature-select-worker.PNG)
  2. En la página **Configuración del servidor** , seleccione la cuenta para ejecutar el servicio **Trabajador de escalado horizontal de SQL Server Integration Services** y, después, seleccione el **tipo de inicio**.    
  ![Configuración de servidor 2](media/server-config-2.PNG "configuración de servidor 2")
  3. En la página **Configuración del trabajador de escalado horizontal de Integration Services** , especifique el punto de conexión para conectarse al patrón de escalado horizontal. 
      > [!Note]
      > Puede omitir la configuración de nodo de trabajo (paso 3 y 4) aquí y asociar la escala fuera trabajo escala Out patrón con [escala Out Manager](integration-services-ssis-scale-out-manager.md) después de la instalación.

    - Para una **un equipo** entorno, el punto de conexión se genera automáticamente cuando se instalan escala Out Master y escala Out trabajo al mismo tiempo. 
    - Para una **varios equipos** entorno, el extremo está compuesto por el nombre o la dirección IP del equipo con escala Out Master instalada y el número de puerto especificado durante la instalación de escala Out Master.    
   ![Configuración de trabajo 1](media/worker-config.PNG "configuración de trabajo 1")    

  4. Para una **varios equipos** entorno, especifique el certificado SSL de cliente que se utiliza para validar la escala fuera Master. Para una **un equipo** entorno, no es necesario especificar el certificado de cliente SSL. 
  
     > [!NOTE]
     > Cuando el certificado SSL usado maestro fuera de la escala es autofirmado, se debe estar instalada en el equipo con escala Out trabajo un certificado SSL de cliente correspondiente. Si proporciona la ruta de acceso de archivo para el certificado SSL de cliente en el **escala Out trabajo configuración de Integration Services** página, el certificado se instalará automáticamente; en caso contrario, tendrá que instalar el certificado manualmente más adelante. 
     
     Haga clic en **Examinar** para buscar el archivo de certificado (*.cer). Para usar el certificado SSL predeterminado, seleccione el archivo SSISScaleOutMaster.cer ubicado en \<unidad\>: \Program Server\140\DTS\Binn de SQL en el equipo donde está instalado escala Out Master.   
   ![Configuración del trabajo 2](media/worker-config-2.PNG "configuración del trabajo 2")
  5. Finalice el Asistente para la instalación de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].
- Pasos para la línea de comandos

    Siga las instrucciones descritas en [Instalar SQL Server desde el símbolo del sistema](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md). Establezca los parámetros relacionados del trabajador de escalado horizontal siguiendo estos pasos.
    1.  Agregue IS_Worker al parámetro /FEATURES.
    2. Configurar escala Out Worker especifica los siguientes parámetros y sus valores: /ISWORKERSVCACCOUNT, /ISWORKERSVCPASSWORD, /ISWORKERSVCSTARTUPTYPE, /ISWORKERSVCMASTER(optional), /ISWORKERSVCCERT(optional).

 
## <a name="InstallCert"></a> Instalar el certificado de cliente del trabajador de escalado horizontal

Durante la instalación de escala a un trabajo, un certificado de trabajo se automáticamente se creará e instalado en el equipo. También se instalará un certificado de cliente correspondiente, SSISScaleOutWorker.cer, en \<unidad\>:\Archivos de programa\Microsoft SQL Server\140\DTS\Binn. Escala Out página maestra autenticar el trabajador de salida de escala, debe agregar este certificado de cliente en el almacén raíz del equipo local con escala Out maestro.
  
Para agregar el certificado de cliente al almacén raíz, haga doble clic en el archivo .cer y, luego, haga clic en **Instalar certificado** en el cuadro de diálogo del certificado. Se abre el **Asistente para importar certificados** .  

## <a name="Firewall"></a> Abrir el puerto del firewall

Abrir el puerto especificado durante la instalación de escala Out maestra y el puerto de SQL Server (1433, de forma predeterminada), con Firewall de Windows en el equipo de escala Out Master.
    
## <a name="Start"></a> Iniciar los servicios de patrón y trabajador de escalado horizontal de SQL Server

Si el tipo de inicio de los servicios no se establece en automático durante la instalación, inicie los servicios: SQL Server Integration Services escala Out Master 14.0 (SSISScaleOutMaster140) y SQL Server Integration Services escala Out trabajo 14.0 (SSISScaleOutWorker140). 

> [!Note]
> Después de abrir el puerto de firewall, debe reiniciar el servicio de escala Out trabajo.
   
## <a name="EnableMaster"></a> Habilitar el patrón de escalado horizontal

Haga clic en **Habilitar este servidor como patrón de escalado horizontal de SSIS** en el cuadro de diálogo **Crear catálogo** al crear el catálogo de SSISDB en [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio_md](../../includes/ssmanstudio-md.md)]. Como alternativa, se puede habilitar la escala fuera Master con [escala Out Manager](integration-services-ssis-scale-out-manager.md) después de crea el catálogo.

## <a name="EnableAuth"></a> Habilitar el modo de autenticación de SQL Server
Si [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] autenticación no está habilitada durante la instalación del motor de base de datos, habilitar el modo de autenticación de SQL Server en el [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] instancia que hospeda el catálogo de SSISDB. 

La ejecución de paquetes no se bloquea si la autenticación de SQL Server está deshabilitada, aunque el registro de ejecución no podrá escribir en SSISDB.

## <a name="EnableWorker"></a> Habilitar el trabajador de escalado horizontal

Escala Out trabajador puede habilitarse a través de [escala Out Manager](integration-services-ssis-scale-out-manager.md), que proporciona la interfaz gráfica de usuario; o habilita a través del procedimiento almacenado, vea a continuación.

Para habilitar el trabajador de escalado horizontal, ejecute el procedimiento almacenado *[catalog].[enable_worker_agent]* con **WorkerAgentId** como parámetro. 

Obtendrá el valor **WorkerAgentId** de la vista de base de datos *[catalog].[worker_agents]* en SSISDB, después de que el trabajador de escalado horizontal se haya registrado en el patrón de escalado horizontal. El registro tarda varios minutos una vez iniciados los servicios de patrón y trabajador de escalado horizontal.

#### <a name="example"></a>Ejemplo
Este ejemplo habilita a la escala fuera Worker en EquipoA.
```tsql
SELECT WorkerAgentId, MachineName FROM [catalog].[worker_agents]
GO
-- Result: --
-- WorkerAgentId                           MachineName  --
-- 6583054A-E915-4C2A-80E4-C765E79EF61D    computerA    --

EXEC [catalog].[enable_worker_agent] '6583054A-E915-4C2A-80E4-C765E79EF61D'
GO 
```
## <a name="next-steps"></a>Pasos siguientes
Ha finalizado la configuración de la característica de escalado horizontal. Ahora puede ejecutar paquetes en horizontalmente. Para obtener más información, consulte [Execute Packages in Integration Services (SSIS) Scale Out](run-packages-in-integration-services-ssis-scale-out.md) (Ejecutar paquetes en el escalado horizontal de Integration Services (SSIS)).
