---
title: Instalación de SQL Server Migration Assistant para Access (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 08/15/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- installing SSMA
- instructions, installation
- instructions, upgrade
- licensing SSMA
- prerequisites for installing SSMA
- procedure, installation
- procedure, licensing
- procedure, upgrading
- removing SSMA
- Setup
- uninstalling SSMA
- upgrading SSMA
ms.assetid: dd50eebd-75df-4e0d-8c4d-88b511aae4c7
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 80fc19b17ac1c01f0c57d828a3bc4821050f761d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "75257891"
---
# <a name="installing-sql-server-migration-assistant-for-access-accesstosql"></a>Instalación de SQL Server Migration Assistant para Access (AccessToSQL)
[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant (SSMA) para el acceso se instala mediante un asistente basado en Windows Installer. En este tema se proporciona información sobre los requisitos previos de instalación, un vínculo a la versión más reciente de SSMA e instrucciones para instalar, conceder licencias, desinstalar y actualizar SSMA.  
  
## <a name="prerequisites"></a>Prerequisites  
Antes de instalar SSMA, asegúrese de que el sistema cumple los requisitos siguientes:  
  
-   Windows 7 o una versión posterior, o Windows Server 2008 o una versión posterior.  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)]Windows Installer 3,1 o una versión posterior.  
  
-   La [!INCLUDE[msCoName](../../includes/msconame_md.md)] versión de .NET Framework 4,0 o una versión posterior. La versión .NET Framework 4,0 está disponible en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] disco del producto y con la información de la [Guía de Microsoft .net](https://docs.microsoft.com/dotnet/framework/).
  
-   Acceso a los permisos y suficientes en el equipo que hospeda la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]destino de/SQL Azure dB a la que va a migrar los datos y los objetos de base de datos.  
  
-   Proveedor de Microsoft Data Access Object (DAO) versión 12,0 o 14,0. Puede instalar el proveedor de DAO desde Microsoft Office producto 2010/2007 o descargarlo desde el sitio web de Microsoft.  
  
-   SQL Server el cliente de acceso nativo (SNAC) versión 10,5 y versiones posteriores para la migración a SQL Azure. Puede obtener la versión más reciente de SNAC del [Feature Pack de Microsoft® SQL Server® 2008 R2](https://www.microsoft.com/download/details.aspx?id=16978)  
  
-   4 GB de RAM (recomendado).  
  
## <a name="installing-ssma"></a>Instalación de SSMA  
SSMA es una descarga Web. Para descargar la versión más reciente, consulte la [Página de descarga de SQL Server Migration Assistant](https://aka.ms/ssmaforaccess).  
  
Después de descargar la versión más reciente, debe extraer los archivos de instalación de antes de poder instalar SSMA.

> [!IMPORTANT]  
> -   Desinstale todas las versiones anteriores de SSMA para Access antes de instalar la nueva versión.  
  
**Para instalar SSMA**  
  
1.  Haga doble clic en SSMA para Access *n*. msi, donde *n* es el número de compilación.  
  
2.  En la página de bienvenida, haga clic en **siguiente**.  
  
    Si no tiene instalados los requisitos previos, aparece un mensaje que indica que primero debe instalar los componentes necesarios. Asegúrese de que ha instalado todos los requisitos previos y, a continuación, vuelva a ejecutar el programa de instalación.  
  
3.  Lea el contrato de licencia para el usuario final. Si está de acuerdo, seleccione Acepto **el contrato**y, a continuación, haga clic en **siguiente**.  
  
4.  En la página elegir tipo de instalación, haga clic en **típica**.  
  
5.  Haga clic en **Instalar**.  
  
La ubicación de instalación predeterminada es C:\Archivos de Programa\microsoft SQL Server Migration Assistant para el acceso.  
  
## <a name="uninstalling-ssma-for-access"></a>Desinstalación de SSMA para Access  
Desinstale SSMA mediante **Agregar o quitar programas** en el panel de control. Tenga en cuenta que al desinstalar el programa, no se eliminan los archivos de proyecto o de registro de SSMA.  
  
**Para desinstalar SSMA**  
  
1.  Haga clic en **Inicio**, haga clic en **Panel de Control** y, a continuación, haga clic en **Agregar o quitar programas**.  
  
2.  Seleccione **Microsoft SQL Server Migration Assistant para el acceso**y, a continuación, haga clic en **quitar**.  
  
## <a name="upgrading-to-a-later-version"></a>Actualizar a una versión posterior  
Si desea actualizar a una versión posterior de SSMA para el acceso, primero debe desinstalar SSMA para el acceso y, a continuación, instalar la versión más reciente. Siga las instrucciones de la sección desinstalación de SSMA for Access para completar este proceso.  
  
Si abre un proyecto creado en una versión anterior de SSMA para Access, SSMA le pregunta si desea convertir el proyecto a la versión más reciente. Haga clic en **sí** para trabajar con el proyecto en la versión más reciente de SSMA.  
  
## <a name="see-also"></a>Consulte también  
[Preparación de bases de datos de Access para migración](preparing-access-databases-for-migration-accesstosql.md)  
[Migrar bases de datos de Access a SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[Vincular aplicaciones de Access a SQL Server](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md)  
  
