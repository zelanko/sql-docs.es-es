---
title: Establecer la cuenta del servicio para el selector del demonio de filtro completo | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.component: search
ms.reviewer: ''
ms.suite: sql
ms.technology: search
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- full-text search [SQL Server], FDHOST Launcher (MSSQLFDLauncher) service account
- FDHOST Launcher (MSSQLFDLauncher) [SQL Server]
ms.assetid: 3ab1d101-7ae0-488f-9b57-468e2517b737
caps.latest.revision: 50
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 9a04832fab80a2cec3f013445fc366a02125fc20
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
ms.locfileid: "33182311"
---
# <a name="set-the-service-account-for-the-full-text-filter-daemon-launcher"></a>Establecer la cuenta del servicio para el selector del demonio de filtro completo
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
 En este tema se describe cómo establecer o cambiar la cuenta de servicio para el servicio Selector del demonio de filtro de texto completo de SQL Server (MSSQLFDLauncher) mediante el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La cuenta de servicio predeterminada usada por el programa de instalación de SQL Server es `NT Service\MSSQLFDLauncher`.
  
  
## <a name="about-the-sql-full-text-filter-daemon-launcher-service"></a>Acerca del servicio del Selector de demonio de filtro de texto completo de SQL
La búsqueda de texto completo usa el servicio Selector de demonio de filtro de texto completo de SQL para iniciar el proceso de host de demonio de filtro, que administra las operaciones de filtrado y separación de palabras de la búsqueda de texto completo. Este servicio debe estar ejecutándose para poder usar la búsqueda de texto completo.  
  
El servicio Selector del demonio de filtro de texto completo de SQL Server es un servicio que reconoce instancias y que está asociado a una instancia específica de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El servicio Selector de demonio de filtro de texto completo de SQL propaga la información de la cuenta de servicio a cada proceso de host de demonio de filtro que inicia.  

##  <a name="setting"></a> Establecer la cuenta de servicio  
  
1.  En el menú **Inicio**, seleccione **Todos los programas**, expanda [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)] y, luego, haga clic en **Administrador de configuración de SQL Server 2016**.  
  
2.  En **Administrador de configuración de SQL Server**, haga clic en **Servicios de SQL Server**, haga clic con el botón derecho en **Selector de demonio de filtro de texto completo de SQL (***nombre de instancia***)** y luego haga clic en **Propiedades**.  
  
3.  Haga clic en la pestaña **Iniciar sesión** del cuadro de diálogo y, luego, seleccione o escriba la cuenta en la que se van a ejecutar los procesos que inicia el servicio Selector de demonio de filtro de texto completo de SQL.  
  
4.  Después de cerrar el cuadro de diálogo, haga clic en **Reiniciar** para reiniciar el servicio Selector de demonio de filtro de texto completo de SQL.  
  
![Propiedades del proceso del Selector de demonio de filtro de texto completo de SQL](../../relational-databases/search/media/sql-full-text-filter-daemon-launch-process-properties.png)
  
##  <a name="error"></a> Solucionar problemas del servicio del Selector de demonio de filtro de texto completo de SQL si no se inicia  
 Si el servicio del Selector de demonio de filtro de texto completo de SQL no se inicia, revise las siguientes causas posibles:  
  
### <a name="permissions-issues"></a>Problemas de permisos
-   El grupo de servicio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no tiene permiso para iniciar el servicio Selector de demonio de filtro de texto completo de SQL.  

     Asegúrese de que el grupo de servicios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tenga permisos para la cuenta de servicio del Selector de demonio de filtro de texto completo de SQL. Durante la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], al grupo de servicios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se le concede el permiso predeterminado para administrar, consultar e iniciar el servicio Selector del demonio de filtro de texto completo de SQL. Si los permisos del grupo de servicios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para la cuenta del servicio Selector de demonio de filtro de texto completo de SQL se han quitado después de la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , dicho servicio no se iniciará y la búsqueda de texto completo se deshabilitará.     

-   La cuenta que se usó para iniciar sesión en el servicio no tiene privilegios.  
  
     Es posible que esté usando una cuenta que no tenga privilegios de inicio de sesión en el equipo donde está instalada la instancia del servidor. Compruebe que está iniciando sesión con una cuenta que tiene derechos y permisos de usuario en el equipo local.  

### <a name="service-account-and-password-issues"></a>Problemas con la cuenta y la contraseña del servicio
-   La cuenta de usuario o contraseña de la cuenta de servicio es incorrecta.  
  
     En el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016, asegúrese de que el servicio usa la cuenta y la contraseña del servicio correctas.  
  
-   La contraseña asociada a la cuenta del servicio Selector del demonio de filtro de texto completo de SQL ha expirado.  
  
     Si usa una cuenta de usuario local para el servicio Selector del demonio de filtro de texto completo de SQL y la contraseña expira, deberá:  
  
    1.  Establecer una nueva contraseña de Windows para la cuenta.  
  
    2.  En el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016, actualice el servicio del Selector de demonio de filtro de texto completo de SQL de modo que use la nueva contraseña.  
  
### <a name="named-pipes-configuration-issues"></a>Problemas con la configuración de las canalizaciones con nombre
-   El servicio Selector del demonio de filtro de texto completo de SQL no está configurado correctamente.  
  
     Si la funcionalidad de canalizaciones con nombre se ha deshabilitado en el equipo local, o si [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se ha configurado para usar una canalización con nombre distinta de la predeterminada, el servicio Selector de demonio de filtro de texto completo de SQL podría no iniciarse.  
  
-   Otra instancia de la misma canalización con nombre ya se está ejecutando.  
  
     El servicio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] actúa como servidor de canalizaciones con nombre para el cliente del servicio Selector del demonio de filtro de texto completo de SQL. Si otro proceso ya creó la canalización con nombre antes de que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se inicie, se grabará un error en el registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y en el registro de eventos de Windows, y la búsqueda de texto completo no estará disponible.  Averigüe qué proceso o aplicación está intentando utilizar la misma canalización con nombre y detenga la aplicación.  
  
## <a name="see-also"></a>Ver también  
 [Temas de procedimientos de administración de servicios &#40;Administrador de configuración de SQL Server&#41;](http://msdn.microsoft.com/library/78dee169-df0c-4c95-9af7-bf033bc9fdc6)   
 [Actualizar la búsqueda de texto completo](../../relational-databases/search/upgrade-full-text-search.md)  
  
  
