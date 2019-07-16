---
title: Instalación de SSMA para el cliente de MySQL (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Installing client,Licensing
ms.assetid: ede3128c-370d-45a5-a815-3d94eecaea30
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 9dcdeaff1c4782453a9fd57cc709e17ad3200d28
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086824"
---
# <a name="installing-ssma-for-mysql-client-mysqltosql"></a>Instalación del cliente de SSMA para MySQL (MySQLToSQL)
SSMA para MySQL cliente consta de los archivos de programa que realizan las siguientes tareas:  
  
-   Conectarse a una base de datos MySQL.  
  
-   Conectarse a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure.  
  
-   Convertir los objetos de base de datos de MySQL para el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] u objetos de SQL Azure.  
  
-   Cargar los objetos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure.  
  
-   Migrar datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure.  
  
Este tema proporciona instrucciones para la instalación de SSMA para MySQL cliente los requisitos previos de instalación.  
  
## <a name="prerequisites"></a>Requisitos previos  
SSMA para MySQL está diseñado para trabajar con MySQL 4.1 o versiones posteriores y todas las ediciones de SQL Server 2005, SQL Server 2008, SQL Server 2012, SQL Server 2014, SQL Server 2016, SQL Server 2017 y Azure SQL DB.  
  
Antes de instalar SSMA, asegúrese de que el equipo cumple los requisitos siguientes:  
  
-   Windows 7 o versiones posteriores, o Windows Server 2008 o versiones posteriores.  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 o una versión posterior.  
  
-   El [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] versión 4.0 o una versión posterior. El [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] versión 4.0 está disponible en el disco del producto de SQL Server. También puede obtener desde el [Centro para desarrolladores de .NET Framework](https://go.microsoft.com/fwlink/?LinkId=48882).  
  
-   Controlador ODBC 5.1 de MySQL y la conectividad a las bases de datos MySQL que se van a migrar. Puede instalar MySQL desde el sitio MySQL Web. Para obtener información acerca de la conectividad, consulte [conectar con MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
  
-   Acceso a y los permisos necesarios en el equipo que hospeda la instancia de SQL Server donde va a migrar datos y objetos de base de datos de destino. Para obtener más información, consulte [conectarse a SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  
-   En el caso de los proyectos de SQL Azure, acceso a y los permisos necesarios a la instancia de Azure SQL DB donde va a migrar objetos y datos de base. Para obtener más información, consulte [conexión a Azure SQL DB &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-azure-sql-db-mysqltosql.md).  
  
-   4 GB de RAM recomendado.  
  
## <a name="installing-ssma-for-mysql-client"></a>Instalar SSMA para el cliente de MySQL  
SSMA es una descarga Web. Para descargar la versión más reciente, consulte el [página de descarga de SQL Server Migration Assistant](https://aka.ms/ssmaformysql).  
  
Después de descargar la versión más reciente, debe extraer los archivos de instalación antes de poder instalar SSMA.  
  
**Para instalar al cliente SSMA**  
  
1.  Haga doble clic en SSMA para MySQL *n*. Install.exe, donde *n* es el número de compilación.  
  
2.  En la página de bienvenida, haga clic en **siguiente**.  
  
    Si no tiene instalados los requisitos previos, aparecerá un mensaje que indica que primero debe instalar los componentes necesarios. Asegúrese de que ha instalado todos los requisitos previos antes de ejecutar el programa de instalación de nuevo.  
  
3.  Lea el contrato de licencia de usuario final. Si está de acuerdo, seleccione **acepto los términos del contrato de licencia**y, a continuación, haga clic en **siguiente**.  
  
4.  En la página Elegir tipo de instalación, haga clic en **típica**.  
  
5.  Haga clic en **Instalar**.  
  
> [!IMPORTANT]  
> 1.  Desinstale todas las versiones anteriores de SSMA para MySQL antes de instalar la nueva versión.  
  
La ubicación de instalación predeterminada es C:\Program Files\Microsoft SQL Server Migration Assistant para MySQL.  
  
En el equipo de Windows de 64 bits, el producto está instalado en C:\Microsoft SQL Server Migration Assistant para MySQL.  
  
## <a name="see-also"></a>Vea también  
[Bases de datos de migración desde MySQL a SQL Server: base de datos SQL Azure &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
