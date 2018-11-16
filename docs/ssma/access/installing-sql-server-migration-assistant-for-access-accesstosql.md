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
manager: craigg
ms.openlocfilehash: 128c83e0fd63b2724311aec046bdb9683c569a03
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/15/2018
ms.locfileid: "51664124"
---
# <a name="installing-sql-server-migration-assistant-for-access-accesstosql"></a>Instalación de SQL Server Migration Assistant para Access (AccessToSQL)
[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant (SSMA) para el acceso se instala mediante un asistente basado en Windows Installer. Este tema proporciona información sobre los requisitos previos de instalación, un vínculo a la versión más reciente de SSMA e instrucciones para instalar, licencias, desinstalar y actualizar SSMA.  
  
## <a name="prerequisites"></a>Requisitos previos  
Antes de instalar SSMA, asegúrese de que su sistema cumple los requisitos siguientes:  
  
-   Windows 7 o una versión posterior, o Windows Server 2008 o una versión posterior.  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 o una versión posterior.  
  
-   El [!INCLUDE[msCoName](../../includes/msconame_md.md)] .NET Framework versión 4.0 o una versión posterior. La versión 4.0 de .NET Framework está disponible en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] disco del producto y con información de la [Guía de .NET de Microsoft](https://docs.microsoft.com/dotnet/framework/).
  
-   Acceso a y los permisos necesarios en el equipo que hospeda la instancia de destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]a la que va a migrar datos y objetos de base de datos de SQL Azure DB.  
  
-   Microsoft Data Access Object (DAO) versión 12.0 o 14.0 del proveedor. Puede instalar al proveedor de DAO de producto de Microsoft Office 2010 o 2007 o descargarlo desde el sitio web de Microsoft.  
  
-   El SQL Server Native Access Client (SNAC) versión 10.5 y posterior para la migración a SQL Azure. Puede obtener la última versión de SNAC desde [Feature Pack de Microsoft® SQL Server® 2008 R2](https://go.microsoft.com/fwlink/?LinkId=196940)  
  
-   4 GB de RAM (recomendado).  
  
## <a name="installing-ssma"></a>Instalación de SSMA  
SSMA es una descarga Web. Para descargar la versión más reciente, consulte el [página de descarga de SQL Server Migration Assistant](https://aka.ms/ssmaforaccess).  
  
Después de descargar la versión más reciente, debe extraer los archivos de instalación desde antes de poder instalar SSMA.

> [!IMPORTANT]  
> -   Desinstale todas las versiones anteriores de SSMA para Access antes de instalar la nueva versión.  
  
**Para instalar SSMA**  
  
1.  Haga doble clic en SSMA para Access *n*.msi, donde *n* es el número de compilación.  
  
2.  En la página de bienvenida, haga clic en **siguiente**.  
  
    Si no tiene instalados los requisitos previos, aparece un mensaje que indica que primero debe instalar los componentes necesarios. Asegúrese de que ha instalado todos los requisitos previos y, a continuación, ejecute el programa de instalación de nuevo.  
  
3.  Lea el contrato de licencia del usuario final; Si está de acuerdo, seleccione **acepto el contrato**y, a continuación, haga clic en **siguiente**.  
  
4.  En la página Elegir tipo de instalación, haga clic en **típica**.  
  
5.  Haga clic en **Instalar**.  
  
La ubicación de instalación predeterminada es C:\Program Files\Microsoft SQL Server Migration Assistant para Access.  
  
## <a name="uninstalling-ssma-for-access"></a>Desinstalación de SSMA para Access  
Desinstalar SSMA mediante **agregar o quitar programas** en el Panel de Control. Tenga en cuenta que al desinstalar el programa no eliminar archivos del proyecto SSMA o los archivos de registro.  
  
**Para desinstalar SSMA**  
  
1.  Haga clic en **iniciar**, haga clic en **Panel de Control**y, a continuación, haga clic en **agregar o quitar programas**.  
  
2.  Seleccione **Microsoft SQL Server Migration Assistant para Access**y, a continuación, haga clic en **quitar**.  
  
## <a name="upgrading-to-a-later-version"></a>Actualizar a una versión posterior  
Si desea actualizar a una versión posterior de SSMA para Access, debe desinstalar primero SSMA para Access y, a continuación, instale la versión más reciente. Siga las instrucciones de desinstalación de SSMA para la sección acceso para completar este proceso.  
  
Si abre un proyecto creado en una versión anterior de SSMA para Access, SSMA le pregunta si desea convertir el proyecto a la versión más reciente. Haga clic en **Sí** para trabajar con el proyecto en la versión más reciente de SSMA.  
  
## <a name="see-also"></a>Vea también  
[Preparar las bases de datos de acceso para la migración](preparing-access-databases-for-migration-accesstosql.md)  
[Migrar bases de datos de Access a SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[Vinculación de aplicaciones de acceso a SQL Server](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md)  
  
