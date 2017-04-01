---
title: "Establecer las propiedades del servicio Integration Services | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "servicio de Integration Services, configurar"
  - "servicio de Integration Services, propiedades"
ms.assetid: 3a8ad546-0f58-4b31-ab56-58d6313b1098
caps.latest.revision: 31
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 31
---
# Establecer las propiedades del servicio Integration Services
    
> [!IMPORTANT]  
>  En este tema se describe el servicio de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , un servicio Windows para administrar paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] admite el servicio para mantener la compatibilidad con versiones anteriores de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. A partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], puede administrar objetos como paquetes en el servidor de Integration Services.  
  
 El servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] administra y supervisa los paquetes de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Al instalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]por primera vez, se inicia el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] y el tipo de inicio del servicio se establece como automático.  
  
 Una vez instalado el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], puede establecer sus propiedades mediante el Administrador de configuración de SQL Server o el complemento Servicios de componentes de MMC.  
  
 Para configurar otras características importantes del servicio, incluidas las ubicaciones donde almacena y administra los paquetes, debe modificar el archivo de configuración del servicio. Para obtener más información, vea [Configurar el servicio Integration Services &#40;servicio SSIS&#41;](../../integration-services/service/configuring-the-integration-services-service-ssis-service.md).  
  
### Para establecer las propiedades del servicio Integration Services con el Administrador de configuración de SQL Server  
  
1.  En el menú **Inicio** , seleccione **Todos los programas**, **Microsoft SQL Server**, **Herramientas de configuración**y haga clic en **Administrador de configuración de SQL Server**.  
  
2.  En el complemento **Administrador de configuración de SQL Server**, busque **SQL Server Integration Services** en la lista de servicios, haga clic con el botón derecho en **SQL Server Integration Services** y, después, haga clic en **Propiedades**.  
  
3.  En el cuadro de diálogo **Propiedades de SQL Server Integration Services** , puede hacer lo siguiente:  
  
    -   Haga clic en la pestaña **Iniciar sesión** para ver la información de inicio de sesión, como el nombre de cuenta.  
  
    -   Haga clic en la pestaña **Servicio** para ver información sobre el servicio, como el nombre del equipo host y para especificar el modo de inicio del servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
        > [!NOTE]  
        >  La pestaña **Avanzadas** no contiene información para el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
4.  Haga clic en **Aceptar**.  
  
5.  En el menú **Archivo**, haga clic en **Salir** para cerrar el complemento **Administrador de configuración de SQL Server**.  
  
### Para establecer las propiedades del servicio Integration Services con el complemento Servicios  
  
1.  En el **Panel de control**, si utiliza la Vista clásica, haga clic en **Herramientas administrativas**o bien, si utiliza la Vista por categorías, haga clic en **Rendimiento y mantenimiento** y, a continuación, en **Herramientas administrativas**.  
  
2.  Haga clic en **Servicios**.  
  
3.  En el complemento **Servicios**, localice **SQL Server Integration Services** en la lista de servicios, haga clic con el botón derecho en **SQL Server Integration Services** y, después, haga clic en **Propiedades**.  
  
4.  En el cuadro de diálogo **Propiedades de SQL Server Integration Services** , puede hacer lo siguiente:  
  
    -   Haga clic en la pestaña **General** . Para habilitar el servicio, seleccione el tipo de inicio manual o automático. Para deshabilitar el servicio, seleccione Deshabilitar en el cuadro **Tipo de inicio** . Si el servicio se está ejecutando, no se detendrá al seleccionar Deshabilitar.  
  
         Si el servicio ya está habilitado, puede hacer clic en **Detener** para detenerlo o en **Iniciar** para iniciarlo.  
  
    -   Haga clic en la pestaña **Iniciar sesión** para ver o editar la información de inicio de sesión.  
  
    -   Haga clic en la pestaña **Recuperación** para ver las respuestas predeterminadas del equipo a un error en el servicio. Puede modificar estas opciones para adaptarlas a su entorno.  
  
    -   Haga clic en la pestaña **Dependencias** para ver una lista de los servicios dependientes. El servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no tiene dependencias.  
  
5.  Haga clic en **Aceptar**.  
  
6.  Opcionalmente, si el tipo de inicio es Manual o Automático, puede hacer clic con el botón derecho en **SQL Server Integration Services ** y hacer clic en **Iniciar, Detener o Reiniciar**.  
  
7.  En el menú **Archivo**, haga clic en **Salir** para cerrar el complemento **Servicios**.  
  
## Vea también  
 [Administrar el servicio Integration Services](../../integration-services/service/manage-the-integration-services-service.md)  
  
  