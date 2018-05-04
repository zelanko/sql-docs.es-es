---
title: Instalación de SSMA para Sybase cliente (SybaseToSQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: e770c2f2-52b9-4471-a207-0d35df41399c
caps.latest.revision: 18
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: c4b98993154780f6d7671d820ad24267b39e2b00
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="installing-ssma--for-sybase-client-sybasetosql"></a>Instalación de SSMA para Sybase cliente (SybaseToSQL)
El cliente SSMA consta de los archivos de programa que se usan para conectarse a un servidor de base de datos de Sybase Adaptive Server Enterprise (ASE) y una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o base de datos de SQL Azure, convertir objetos de base de datos de ASE a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o la sintaxis de la base de datos de SQL Azure, cargue los objetos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o base de datos de SQL Azure, y, a continuación, migrar datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQLDB de Azure.  
  
Este tema proporciona los requisitos previos de instalación e instrucciones para la instalación de SSMA.  
  
## <a name="prerequisites"></a>Requisitos previos  
SSMA está diseñado para trabajar con ASE 11.9.2 o versiones posteriores y todas las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
Antes de instalar SSMA, asegúrese de que el equipo cumple los requisitos siguientes:  
  
-   Windows 7 o versiones posteriores, o Windows Server 2008 o versiones posteriores.  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 o una versión posterior.  
  
-   El [!INCLUDE[msCoName](../../includes/msconame_md.md)] .NET Framework versión 4.0 o una versión posterior. La versión 4.0 de .NET Framework está disponible en la [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] CD del producto. También puede obtener desde la [Centro para desarrolladores de .NET Framework](http://go.microsoft.com/fwlink/?LinkId=48882).  
  
-   El proveedor de Sybase OLEDB/ADO.Net/ODBC y la conectividad con el servidor de base de datos de Sybase ASE que contiene las bases de datos que van a migrar. Puede instalar a proveedores desde el CD del producto de Sybase ASE. Para obtener información acerca de la conectividad, vea [conectarse para Sybase ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md).  
  
-   Acceso y permisos suficientes en el equipo que hospeda la instancia de destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o base de datos de SQL de Azure donde se va a migrar datos y objetos de base de datos. Para obtener más información, consulte [conectarse a SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sql-server-sybasetosql.md)/[conectarse a la base de datos de SQL Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-azure-sql-db-sybasetosql.md).  
  
-   4 GB de RAM recomendado.  
  
## <a name="installing-the-ssma-for-sybase-client"></a>Instalación de SSMA para Sybase cliente  
SSMA es una descarga Web. Para descargar la versión más reciente, consulte el [página de descarga de SQL Server Migration Assistant](http://aka.ms/ssmaforsybase).  
  
Después de descargar la versión más reciente, debe extraer los archivos de instalación de para poder instalar SSMA.  
  
**Para instalar al cliente SSMA**  
  
1.  Haga doble clic en SSMA para Sybase *n*. Install.exe, donde *n* es el número de compilación.  
  
2.  En la página de bienvenida, haga clic en **siguiente**.  
  
    Si no tiene los requisitos previos instalados, aparecerá un mensaje que indica que primero debe instalar los componentes necesarios. Asegúrese de que ha instalado todos los requisitos previos y, a continuación, ejecute de nuevo el programa de instalación.  
  
3.  Lea el contrato de licencia de usuario final. Si los acepta, seleccione **acepto los términos del contrato de licencia**y, a continuación, haga clic en **siguiente**.  
  
4.  En la página Elegir tipo de instalación, haga clic en **típica**.  
  
5.  Haga clic en **Instalar**.  
  
> [!IMPORTANT]  
> 1.  Desinstale todas las versiones anteriores de SSMA para Sybase antes de instalar la nueva versión.  
  
La ubicación de instalación predeterminada es C:\Program Files\Microsoft SQL Server Migration Assistant para Sybase.  
  
Además de los archivos de programa SSMA, también debe instalar SSMA para Sybase: paquete de extensión en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] . Para obtener más información, consulte [instalar componentes de SSMA en SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md).  
  
## <a name="see-also"></a>Vea también  
[Instalar componentes SSMA en SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)  
[Migrar bases de datos de Sybase ASE a SQL Server: base de datos de SQL Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
