---
title: Instalar PowerPivot desde el símbolo | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 7f1f2b28-c9f5-49ad-934b-02f2fa6b9328
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: e84b6e148774fc9b48b6174fa8be87579290fec4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62657329"
---
# <a name="install-powerpivot-from-the-command-prompt"></a>Instalar PowerPivot desde el símbolo del sistema
  Puede ejecutar el programa de instalación desde la línea de comandos para instalar SQL Server PowerPivot para SharePoint. Debe incluir el parámetro `/ROLE` en el comando y excluir el parámetro `/FEATURES`.  
  
## <a name="prerequisites"></a>Requisitos previos  
 Debe estar instalada la versión Enterprise de SharePoint Server 2010 con Service Pack 1 (SP1).  
  
 Debe utilizar las cuentas de dominio para aprovisionar a Analysis Services.  
  
 El equipo debe estar unido al mismo dominio que la granja de servidores de SharePoint.  
  
##  <a name="Commands"></a> Opciones de instalación basadas en /Role  
 En las implementaciones de PowerPivot para SharePoint, se utiliza el parámetro `/ROLE` en lugar de `/FEATURES`. Los valores válidos incluyen:  
  
-   `SPI_AS_ExistingFarm`  
  
-   `SPI_AS_NewFarm`  
  
 Ambos roles instalan los archivos de aplicación, configuración e implementación que permiten que PowerPivot para SharePoint se ejecute en una granja de SharePoint. Si se especifica uno de los dos roles, el programa de instalación comprobará los requisitos de hardware y software necesarios para la integración de SharePoint.  
  
 La opción de granja existente supone que ya hay una granja de servidores de SharePoint. La nueva opción de granja de servidores, se da por supuesto que va a crear una nueva granja; admite la adición de una instancia del motor de base de datos en la sintaxis de línea de comandos para que pueda usar la instancia del motor de base de datos como servidor de base de datos de la granja de servidores.  
  
 A diferencia de las versiones anteriores, todas las tareas de configuración del servidor se realizan como tareas posteriores a la instalación. Si está automatizando los pasos de instalación y configuración, puede utilizar PowerShell para configurar el servidor. Para obtener más información, consulte [configuración de PowerPivot mediante Windows PowerShell](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-using-windows-powershell.md).  
  
## <a name="example-commands"></a>Comandos de ejemplo  
 Los siguientes ejemplos ilustran el uso de cada opción. Se muestra en el ejemplo 1 `SPI_AS_ExistingFarm`.  
  
```  
Setup.exe /q /IAcceptSQLServerLicenseTerms /ACTION=install /ROLE=SPI_AS_ExistingFarm /INSTANCENAME=PowerPivot /INDICATEPROGRESS/ASSVCACCOUNT=<DomainName\UserName> /ASSVCPASSWORD=<StrongPassword> /ASSYSADMINACCOUNTS=<DomainName\UserName>   
```  
  
 El ejemplo 2 muestra `SPI_AS_NewFarm`. Observe que incluye los parámetros para aprovisionar al Motor de base de datos.  
  
```  
Setup.exe /q /IAcceptSQLServerLicenseTerms /ACTION=install /ROLE=SPI_AS_NewFarm /INSTANCENAME=PowerPivot /INDICATEPROGRESS/SQLSVCACCOUNT=<DomainName\UserName> /SQLSVCPASSWORD=<StrongPassword> /SQLSYSADMINACCOUNTS=<DomainName\UserName> /AGTSVCACCOUNT=<DomainName\UserName> /AGTSVCPASSWORD=<StrongPassword> /ASSVCACCOUNT=<DomainName\UserName> /ASSVCPASSWORD=<StrongPassword> /ASSYSADMINACCOUNTS=<DomainName\UserName>   
```  
  
##  <a name="Join"></a> Modificar la sintaxis del comando  
 Utilice los siguientes pasos para modificar la sintaxis del comando del ejemplo.  
  
1.  Copie el siguiente comando en el Bloc de notas:  
  
    ```  
    Setup.exe /q /IAcceptSQLServerLicenseTerms /ACTION=install /ROLE=SPI_AS_ExistingFarm /INSTANCENAME=PowerPivot /INDICATEPROGRESS/ASSVCACCOUNT=<DomainName\UserName> /ASSVCPASSWORD=<StrongPassword> /ASSYSADMINACCOUNTS=<DomainName\UserName>   
    ```  
  
     El parámetro `/q` ejecuta el programa de instalación en modo silencio, que suprime la interfaz de usuario.  
  
     `/IAcceptSQLServerLicenseTerms` es necesario cuando se especifican los parámetros `/q` o `/qs` para instalaciones desatendidas.  
  
     El parámetro `/action` indica al programa de instalación que realice una instalación.  
  
     El parámetro `/role` indica al programa de instalación que instale el programa de Analysis Services y los archivos de configuración necesarios para PowerPivot para SharePoint. Este rol también detecta y utiliza la información de conectividad de granja existente para tener acceso a la base de datos de configuración de SharePoint. Este parámetro es obligatorio. Úselo en lugar del parámetro `/features` para especificar qué componentes se deben instalar.  
  
     El parámetro `/instancename` especifica 'PowerPivot' como una instancia con nombre. Este valor está codificado de forma rígida y no se puede cambiar. Se especifica en el comando únicamente para que sepa cómo se instala el servicio.  
  
     El parámetro `/indicateprogress` le permite supervisar el progreso en la ventana del símbolo del sistema.  
  
2.  El parámetro `PID` se omite del comando, que hace que se instale la edición de evaluación. Si desea instalar la edición Enterprise, agregue el PID al comando del programa de instalación y proporcione una clave del producto válida.  
  
    ```  
  
    /PID=<product key for an Enterprise installation>  
  
    ```  
  
3.  Reemplace los marcadores de posición para \<dominio\nombre de usuario > y \<contraseña segura > con cuentas de usuario válidas y las contraseñas.  
  
     El `/assvaccount` y **/assvcpassword** parámetros se usan para configurar el [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] instancia del servidor de aplicaciones. Reemplace estos marcadores de posición con información de cuenta válida.  
  
     El **/assysadminaccounts** parámetro debe establecerse en la identidad del usuario que se está ejecutando el programa de instalación de SQL Server. Debe especificar al menos un administrador del sistema. Tenga en cuenta que el programa de instalación de SQL Server no concede permisos de sysadmin automáticos a los miembros del grupo de administradores integrado.  
  
4.  Quite los saltos de línea.  
  
5.  Seleccione el comando completo y, a continuación, haga clic en **copia** en el menú Edición.  
  
6.  Abra un símbolo del sistema de administrador. Para ello, haga clic en **iniciar**, haga clic en el símbolo del sistema y seleccione **ejecutar como administrador**.  
  
7.  Navegue hasta la unidad o carpeta compartida que contiene el disco de instalación de SQL Server.  
  
8.  Pegue el comando revisado en la línea de comandos. Para ello, haga clic en el icono en la esquina superior izquierda de la ventana de símbolo del sistema, **editar**y, a continuación, haga clic en **pegar**.  
  
9. Presione **ENTRAR** para ejecutar el comando. Espere a que termine la instalación. Puede supervisar el progreso del programa de instalación en la ventana del símbolo del sistema.  
  
10. Para comprobar la instalación, compruebe el archivo summary.txt en \Archivos de programa\SQL Server\120\Setup Bootstrap\Log. El resultado final debe decir "Passed" si el servidor se instaló sin errores.  
  
11. Configure el servidor. Como mínimo, debe implementar soluciones, crear una aplicación de servicio y habilitar la característica para cada colección de sitios. Para obtener más información, consulte [configurar o reparar PowerPivot para SharePoint 2010 &#40;herramienta de configuración de PowerPivot&#41; ](../../../2014/analysis-services/configure-repair-powerpivot-sharepoint-2010.md) o [administración de servidores de PowerPivot y la configuración en Administración Central ](../../analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md).  
  
## <a name="see-also"></a>Vea también  
 [Configurar cuentas de servicio PowerPivot](../../analysis-services/power-pivot-sharepoint/configure-power-pivot-service-accounts.md)   
 [Instalación de PowerPivot para SharePoint 2010](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
  
  
