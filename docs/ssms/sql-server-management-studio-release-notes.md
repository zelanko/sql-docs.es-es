---
title: "SQL Server Management Studio: notas de la versión | Microsoft Docs"
ms.custom: 
ms.date: 01/30/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0b95337b-80bf-4624-8f5d-cdaf6181d3b8
caps.latest.revision: 51
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 51e336a22d0c1052c48b8e569330aef26f2af094
ms.contentlocale: es-es
ms.lasthandoff: 04/11/2017

---
# <a name="sql-server-management-studio----release-notes"></a>SQL Server Management Studio: notas de la versión
Bienvenido/a a nuestra versión de disponibilidad general de SQL Server Management Studio.  Esta versión de SQL Server Management Studio (SSMS) es una instalación independiente fuera de la versión de SQL Server. Nuestro objetivo es actualizarla con frecuencia con nuevas funciones, correcciones y compatibilidad para las características más recientes de SQL Server y de Base de datos SQL de Azure.  
  
Para instalar la versión más reciente de SQL Server Management Studio, vea [Download SQL Server Management Studio &#40;SSMS&#41;](../ssms/download-sql-server-management-studio-ssms.md).  
  
A continuación indicamos los problemas y las limitaciones de esta versión de SQL Server Management Studio:  

1. **Una sola cuenta de Azure Active Directory puede iniciar sesión para una instancia de SSMS utilizando la autenticación universal de Active Directory.**  
    Esta restricción se limita a la autenticación universal de Active Directory. Puede iniciar sesión en servidores diferentes mediante la autenticación de contraseña de Active Directory, la autenticación integrada de Active Directory o la autenticación de SQL Server.
    
    Como alternativa, puede utilizar otra instancia de SSMS para iniciar sesión con otra cuenta de Azure Active Directory. 
    
2. **Los comandos del marco de aplicación de capa de datos (DacFx) y el Diseñador de esquemas en SSMS no admiten la autenticación universal de Active Directory.**  
    Los comandos que utiliza DacFx (por ejemplo, importar y exportar) y el Diseñador de esquemas en SSMS no admiten actualmente la autenticación universal de Active Directory.
    
    Como solución alternativa, puede usar las otras formas de autenticación proporcionada en SSMS - autenticación de contraseña de Active Directory, la autenticación integrada de Active Directory o la autenticación de SQL Server.

3. **SSMS solo puede conectarse a instancias de SQL Server 2016 Integrated Services (SSIS 2016).**  
    Hay una limitación de compatibilidad conocida con SQL Server Integration Services que impide la conexión a versiones anteriores.
    
    Como solución alternativa para este problema, puede conectarse a la instancia de SQL Server Integration Service mediante la [versión SSMS alineado con la instancia SSIS.](../ssms/previous-sql-server-management-studio-releases.md) 
  
4. **SSMS no guardará los planes de mantenimiento de SQL Server 2008 R2 y versiones anteriores de SQL Server.**  
    Se trata de una limitación conocida que esperamos solucionar en el futuro. Mientras tanto, puede usar la [versión de SSMS de 2014](../ssms/previous-sql-server-management-studio-releases.md) para guardar los planes de mantenimiento.  
    
5. **Las instalaciones de SSMS que no estén en inglés pueden requerir la instalación de un paquete de seguridad adicional.**  
Las versiones localizadas de SSMS en idiomas diferentes al inglés requieren el [paquete de actualización de seguridad KB 2862966](https://support.microsoft.com/en-us/kb/2862966) si se instalan en Windows 8, Windows 7, Windows Server 2012 y Windows Server 2008 R2.
  
6. **Administrador de configuración de SQL Server no se iniciará si no hay ningún servidor de SQL Server instalado en el equipo cliente**  
    Si no tiene SQL Server instalado en el equipo cliente e inicia el Administrador de configuración de SQL Server, verá el siguiente error:   
     `Cannot connect to WMI provider. You do not have permission or the server is unreachable. Note that you can only manage SQL Server 2005 and later servers with SQL Server Configuration Manager. Invalid namespace \[0x8004100e]`,   
   
     * Si ha agregado instancias de SQL Server a la lista 'Servidores registrados' en SSMS:  
        1. Desplácese a la vista 'Servidores registrados' en SSMS.  
        2. Haga clic con el botón derecho en la instancia de SQL Server que desee configurar.  
        3. Seleccione 'Administrador de configuración de SQL Server' en el menú de clic con el botón derecho.    
          
      * Si no ha agregado una instancia de SQL Server a la lista 'Servidores registrados' en SSMS:  
        1. Abra un símbolo del sistema como administrador.  
        2. Ejecute la herramienta Mofcomp con el siguiente comando:  
    `mofcomp "%programfiles(x86)%\Microsoft SQL Server\130\Shared\sqlmgmproviderxpsp2up.mof"`  
        3. Después de ejecutar la herramienta Mofcomp, ejecute los comandos para reiniciar el servicio WMI para que los cambios surtan efecto:  
        `net stop "Windows Management Instrumentation"`  
        `net start “Windows Management Instrumentation”`  

## <a name="feedback"></a>Comentarios  
  
![needhelp_person_icon](../ssms/media/needhelp_person_icon.png) [Foro de Herramientas de cliente de SQL](https://social.msdn.microsoft.com/Forums/en-US/home?forum=sqltools) |  [Registre un problema o una sugerencia en Microsoft Connect](https://connect.microsoft.com/SQLServer/Feedback).  
  
## <a name="see-also"></a>Vea también  
[Tutorial de SQL Server Management Studio](../ssms/use-sql-server-management-studio.md)  
[Descargar SQL Server Management Studio &amp;#40;SSMS&amp;#41;](../ssms/download-sql-server-management-studio-ssms.md)  
[Versiones anteriores de SQL Server Management Studio](../ssms/previous-sql-server-management-studio-releases.md)  

  

