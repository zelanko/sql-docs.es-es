---
title: Instalación de SSMA para cliente de MySQL (MySQLToSQL) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-mysql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Installing client,Licensing
ms.assetid: ede3128c-370d-45a5-a815-3d94eecaea30
caps.latest.revision: 22
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: a9ebee93032b97993d670fb37fabea932c3e1302
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="installing-ssma-for-mysql-client-mysqltosql"></a>Instalación de SSMA para cliente de MySQL (MySQLToSQL)
SSMA para cliente de MySQL consta de los archivos de programa que llevan a cabo las siguientes tareas:  
  
-   Conectarse a una base de datos de MySQL.  
  
-   Conéctese a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure.  
  
-   Convertir los objetos de base de datos de MySQL para la [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] u objetos de SQL Azure.  
  
-   Cargar los objetos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure.  
  
-   Migrar datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure.  
  
Este tema proporciona los requisitos previos de instalación e instrucciones para la instalación de SSMA para cliente de MySQL.  
  
## <a name="prerequisites"></a>Requisitos previos  
SSMA para MySQL está diseñado para trabajar con MySQL 4.1 o versiones posteriores y todas las ediciones de SQL Server 2005, SQL Server 2008, SQL Server 2012, SQL Server 2014, SQL Server 2016, SQL Server 2017 y base de datos de SQL Azure.  
  
Antes de instalar SSMA, asegúrese de que el equipo cumple los requisitos siguientes:  
  
-   Windows 7 o versiones posteriores, o Windows Server 2008 o versiones posteriores.  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 o una versión posterior.  
  
-   El [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] versión 4.0 o una versión posterior. El [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] versión 4.0 está disponible en el CD del producto SQL Server. También puede obtener desde la [Centro para desarrolladores de .NET Framework](http://go.microsoft.com/fwlink/?LinkId=48882).  
  
-   Controlador de MySQL ODBC 5.1 y la conectividad a las bases de datos de MySQL que se van a migrar. Puede instalar MySQL desde el sitio MySQL Web. Para obtener información acerca de la conectividad, vea [conectar con MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
  
-   Acceso a y los permisos necesarios en el equipo que hospeda la instancia de destino de SQL Server donde se va a migrar datos y objetos de base de datos. Para obtener más información, consulte [conectarse a SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  
-   En el caso de proyectos de SQL Azure, acceso y los permisos necesarios para la instancia de base de datos de SQL de Azure donde va a migrar objetos y base de datos. Para obtener más información, consulte [conectarse a la base de datos de SQL Azure &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-azure-sql-db-mysqltosql.md).  
  
-   4 GB de RAM recomendado.  
  
## <a name="installing-ssma-for-mysql-client"></a>Instalación de SSMA para cliente de MySQL  
SSMA es una descarga Web. Para descargar la versión más reciente, consulte el [página de descarga de SQL Server Migration Assistant](http://aka.ms/ssmaformysql).  
  
Después de descargar la versión más reciente, debe extraer los archivos de instalación para poder instalar SSMA.  
  
**Para instalar al cliente SSMA**  
  
1.  Haga doble clic en SSMA para MySQL *n*. Install.exe, donde *n* es el número de compilación.  
  
2.  En la página de bienvenida, haga clic en **siguiente**.  
  
    Si no tiene los requisitos previos instalados, aparecerá un mensaje que indica que primero debe instalar los componentes necesarios. Asegúrese de que ha instalado todos los requisitos previos antes de ejecutar el programa de instalación de nuevo.  
  
3.  Lea el contrato de licencia de usuario final. Si los acepta, seleccione **acepto los términos del contrato de licencia**y, a continuación, haga clic en **siguiente**.  
  
4.  En la página Elegir tipo de instalación, haga clic en **típica**.  
  
5.  Haga clic en **Instalar**.  
  
> [!IMPORTANT]  
> 1.  Desinstale todas las versiones anteriores de SSMA para MySQL antes de instalar la nueva versión.  
  
La ubicación de instalación predeterminada es C:\Program Files\Microsoft SQL Server Migration Assistant para MySQL.  
  
En el equipo de Windows de 64 bits se instala el producto en C:\Microsoft SQL Server Migration Assistant para MySQL.  
  
## <a name="see-also"></a>Vea también  
[Bases de datos de migración desde MySQL a SQL Server: base de datos de SQL Azure &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
