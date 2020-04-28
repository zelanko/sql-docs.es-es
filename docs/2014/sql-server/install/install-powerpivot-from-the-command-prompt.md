---
title: Instale PowerPivot desde el símbolo del sistema | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 7f1f2b28-c9f5-49ad-934b-02f2fa6b9328
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 8959b1ca4ea719ce571cb8609b817bba965185bd
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "72798330"
---
# <a name="install-powerpivot-from-the-command-prompt"></a>Instalar PowerPivot desde el símbolo del sistema
  Puede ejecutar el programa de instalación desde la línea de comandos para instalar SQL Server PowerPivot para SharePoint. Debe incluir el parámetro `/ROLE` en el comando y excluir el parámetro `/FEATURES`.  
  
## <a name="prerequisites"></a>Prerrequisitos  
 Debe estar instalada la versión Enterprise de SharePoint Server 2010 con Service Pack 1 (SP1).  
  
 Debe utilizar las cuentas de dominio para aprovisionar a Analysis Services.  
  
 El equipo debe estar unido al mismo dominio que la granja de servidores de SharePoint.  
  
##  <a name="role-based-installation-options"></a><a name="Commands"></a>Opciones de instalación basadas en/ROLE  
 En las implementaciones de PowerPivot para SharePoint, se utiliza el parámetro `/ROLE` en lugar de `/FEATURES`. Los valores válidos son:  
  
-   `SPI_AS_ExistingFarm`  
  
-   `SPI_AS_NewFarm`  
  
 Ambos roles instalan los archivos de aplicación, configuración e implementación que permiten que PowerPivot para SharePoint se ejecute en una granja de SharePoint. Si se especifica uno de los dos roles, el programa de instalación comprobará los requisitos de hardware y software necesarios para la integración de SharePoint.  
  
 La opción de granja existente supone que ya hay una granja de servidores de SharePoint. La nueva opción de granja supone que creará una nueva granja de servidores; admite la adición de una instancia de Motor de base de datos en la sintaxis de la línea de comandos para que pueda usar la instancia de Motor de base de datos como servidor de bases de datos de la granja.  
  
 A diferencia de las versiones anteriores, todas las tareas de configuración del servidor se realizan como tareas posteriores a la instalación. Si está automatizando los pasos de instalación y configuración, puede utilizar PowerShell para configurar el servidor. Para obtener más información, vea [configuración de PowerPivot mediante Windows PowerShell](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-configuration-using-windows-powershell).  
  
## <a name="example-commands"></a>Comandos de ejemplo  
 Los siguientes ejemplos ilustran el uso de cada opción. En el ejemplo `SPI_AS_ExistingFarm`1 se muestra.  
  
```cmd
Setup.exe /q /IAcceptSQLServerLicenseTerms /ACTION=install /ROLE=SPI_AS_ExistingFarm /INSTANCENAME=PowerPivot /INDICATEPROGRESS/ASSVCACCOUNT=<DomainName\UserName> /ASSVCPASSWORD=<StrongPassword> /ASSYSADMINACCOUNTS=<DomainName\UserName>   
```  
  
 El ejemplo 2 muestra `SPI_AS_NewFarm`. Observe que incluye los parámetros para aprovisionar al Motor de base de datos.  
  
```cmd
Setup.exe /q /IAcceptSQLServerLicenseTerms /ACTION=install /ROLE=SPI_AS_NewFarm /INSTANCENAME=PowerPivot /INDICATEPROGRESS/SQLSVCACCOUNT=<DomainName\UserName> /SQLSVCPASSWORD=<StrongPassword> /SQLSYSADMINACCOUNTS=<DomainName\UserName> /AGTSVCACCOUNT=<DomainName\UserName> /AGTSVCPASSWORD=<StrongPassword> /ASSVCACCOUNT=<DomainName\UserName> /ASSVCPASSWORD=<StrongPassword> /ASSYSADMINACCOUNTS=<DomainName\UserName>   
```  
  
##  <a name="modifying-the-command-syntax"></a><a name="Join"></a>Modificar la sintaxis de los comandos  
 Utilice los siguientes pasos para modificar la sintaxis del comando del ejemplo.  
  
1.  Copie el siguiente comando en el Bloc de notas:  
  
    ```cmd
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
  
3.  Reemplace los marcadores de posición \<de dominio\nombre de \<usuario> y StrongPassword>por contraseñas y cuentas de usuario válidas.  
  
     Los `/assvaccount` parámetros y **/assvcpassword** se usan para configurar la [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] instancia en el servidor de aplicaciones. Reemplace estos marcadores de posición con información de cuenta válida.  
  
     El parámetro **/assysadminaccounts** debe establecerse en la identidad del usuario que ejecuta SQL Server el programa de instalación. Debe especificar al menos un administrador del sistema. Tenga en cuenta que el programa de instalación de SQL Server no concede permisos de sysadmin automáticos a los miembros del grupo de administradores integrado.  
  
4.  Quite los saltos de línea.  
  
5.  Seleccione todo el comando y, a continuación, haga clic en **copiar** en el menú edición.  
  
6.  Abra un símbolo del sistema de administrador. Para ello, haga clic en **Inicio**, haga clic con el botón secundario en el símbolo del sistema y seleccione **Ejecutar como administrador**.  
  
7.  Navegue hasta la unidad o carpeta compartida que contiene el disco de instalación de SQL Server.  
  
8.  Pegue el comando revisado en la línea de comandos. Para ello, haga clic en el icono de la esquina superior izquierda de la ventana del símbolo del sistema, seleccione **Editar**y, a continuación, haga clic en **pegar**.  
  
9. Presione **entrar** para ejecutar el comando. Espere a que termine la instalación. Puede supervisar el progreso del programa de instalación en la ventana del símbolo del sistema.  
  
10. Para comprobar la instalación, compruebe el archivo summary.txt en \Archivos de programa\SQL Server\120\Setup Bootstrap\Log. El resultado final debe decir "Passed" si el servidor se instaló sin errores.  
  
11. Configure el servidor. Como mínimo, debe implementar soluciones, crear una aplicación de servicio y habilitar la característica para cada colección de sitios. Para obtener más información, vea [configurar o reparar PowerPivot para SharePoint 2010 &#40;herramienta de configuración de powerpivot&#41;](../../../2014/analysis-services/configure-repair-powerpivot-sharepoint-2010.md) o [Administración y configuración del servidor de PowerPivot en administración central](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration).  
  
## <a name="see-also"></a>Consulte también  
 [Configurar cuentas de servicio PowerPivot](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/configure-power-pivot-service-accounts)   
 [Instalación de PowerPivot para SharePoint 2010](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
