---
title: Instalación de SSMA para el cliente de MySQL (MySQLToSQL) | Microsoft Docs
description: Obtenga información sobre los requisitos previos de instalación para el SQL Server Migration Assistant (SSMA) para el cliente MySQL y cómo instalar.
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
ms.openlocfilehash: bf1a3c8c5a01bb2553f773d5b650805667c116a3
ms.sourcegitcommit: 59cda5a481cfdb4268b2744edc341172e53dede4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2020
ms.locfileid: "84293902"
---
# <a name="installing-ssma-for-mysql-client-mysqltosql"></a>Instalación del cliente de SSMA para MySQL (MySQLToSQL)
SSMA para el cliente de MySQL se compone de los archivos de programa que realizan las siguientes tareas:  
  
-   Conectarse a una base de datos MySQL.  
  
-   Conectarse a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure.  
  
-   Convierta los objetos de base de datos MySQL en los [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objetos o SQL Azure.  
  
-   Cargue los objetos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure.  
  
-   Migrar datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure.  
  
En este tema se proporcionan los requisitos previos de instalación y las instrucciones para instalar SSMA para el cliente de MySQL.  
  
## <a name="prerequisites"></a>Requisitos previos  
SSMA para MySQL está diseñado para funcionar con MySQL 4,1 o versiones posteriores y todas las ediciones de SQL Server 2005, SQL Server 2008, SQL Server 2012, SQL Server 2014, SQL Server 2016, SQL Server 2017 y Azure SQL DB.  
  
Antes de instalar SSMA, asegúrese de que el equipo cumple los requisitos siguientes:  
  
-   Windows 7 o versiones posteriores, o Windows Server 2008 o versiones posteriores.  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)]Windows Installer 3,1 o una versión posterior.  
  
-   La [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] versión 4,0 o una versión posterior. La [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] versión 4,0 está disponible en los medios del producto SQL Server. También puede obtenerlo en el [Centro para desarrolladores de .NET Framework](https://go.microsoft.com/fwlink/?LinkId=48882).  
  
-   Controlador de MySQL ODBC 5,1 y conectividad con las bases de datos de MySQL que desea migrar. Puede instalar MySQL desde el sitio web de MySQL. Para obtener información sobre la conectividad, consulte [conexión a MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
  
-   Acceso a y permisos suficientes en el equipo que hospeda la instancia de destino de SQL Server donde va a migrar los datos y los objetos de base de datos. Para obtener más información, vea [conectarse a SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  
-   En el caso de los proyectos de SQL Azure, acceda a los permisos y suficientes para la instancia de Azure SQL DB en la que va a migrar los datos y los objetos de base de datos. Para obtener más información, consulte [conexión a base de datos SQL de Azure &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-azure-sql-db-mysqltosql.md).  
  
-   se recomiendan 4 GB de RAM.  
  
## <a name="installing-ssma-for-mysql-client"></a>Instalar SSMA para el cliente de MySQL  
SSMA es una descarga Web. Para descargar la versión más reciente, consulte la [Página de descarga de SQL Server Migration Assistant](https://aka.ms/ssmaformysql).  
  
Después de descargar la versión más reciente, debe extraer los archivos de instalación antes de poder instalar SSMA.  
  
**Para instalar el cliente SSMA**  
  
1.  Haga doble clic en SSMA para MySQL *n*.Install.exe, donde *n* es el número de compilación.  
  
2.  En la página de bienvenida, haga clic en **Siguiente**.  
  
    Si no tiene instalados los requisitos previos, aparecerá un mensaje que indica que primero debe instalar los componentes necesarios. Asegúrese de que ha instalado todos los requisitos previos antes de volver a ejecutar el programa de instalación.  
  
3.  Lea el contrato de licencia para el usuario final. Si está de acuerdo, seleccione Acepto **los términos del contrato de licencia**y, a continuación, haga clic en **siguiente**.  
  
4.  En la página elegir tipo de instalación, haga clic en **típica**.  
  
5.  Haga clic en **Instalar**.  
  
> [!IMPORTANT]  
> 1.  Desinstale todas las versiones anteriores de SSMA para MySQL antes de instalar la nueva versión.  
  
La ubicación de instalación predeterminada es C:\Archivos de Programa\microsoft SQL Server Migration Assistant para MySQL.  
  
En el equipo de Windows de 64 bits, el producto se instala en C:\Microsoft SQL Server Migration Assistant para MySQL.  
  
## <a name="see-also"></a>Consulte también  
[Migración de bases de datos de MySQL a SQL Server: Azure SQL DB &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
