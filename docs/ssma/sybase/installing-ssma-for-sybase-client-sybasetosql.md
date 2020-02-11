---
title: Instalación de SSMA para el cliente de Sybase (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: e770c2f2-52b9-4471-a207-0d35df41399c
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 8680685640b234e47f6e68d7fb802fc7e2f5d81c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68029022"
---
# <a name="installing-ssma--for-sybase-client-sybasetosql"></a>Instalación de SSMA para el cliente de Sybase (SybaseToSQL)
El cliente de SSMA está formado por los archivos de programa que se usan para conectarse a un servidor de base de datos de Sybase Adaptive Server Enterprise [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (ASE), una instancia de o Azure SQL [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dB, convertir objetos de base de datos de ase [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en o la sintaxis de Azure SQL Database, cargar los [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objetos en o Azure SQL dB y, a continuación, migrar datos a o a Azure SQLDB.  
  
En este tema se proporcionan los requisitos previos de instalación y las instrucciones para instalar SSMA.  
  
## <a name="prerequisites"></a>Prerequisites  
SSMA está diseñado para funcionar con ASE 11.9.2 o versiones posteriores y todas las ediciones [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]de.  
  
Antes de instalar SSMA, asegúrese de que el equipo cumple los requisitos siguientes:  
  
-   Windows 7 o versiones posteriores, o Windows Server 2008 o versiones posteriores.  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)]Windows Installer 3,1 o una versión posterior.  
  
-   La [!INCLUDE[msCoName](../../includes/msconame_md.md)] versión de .NET Framework 4,0 o una versión posterior. La versión .NET Framework 4,0 está disponible en los [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] medios del producto. También puede obtenerlo en el [Centro para desarrolladores de .NET Framework](https://go.microsoft.com/fwlink/?LinkId=48882).  
  
-   El proveedor de Sybase OLEDB/ADO.Net/ODBC y la conectividad con el servidor de base de datos de Sybase ASE que contiene las bases de datos que desea migrar. Puede instalar proveedores desde los medios del producto Sybase ASE. Para obtener información sobre la conectividad, consulte [conexión a Sybase ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md).  
  
-   Acceso y permisos suficientes en el equipo que hospeda la instancia de destino de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Azure SQL dB, donde se van a migrar los datos y los objetos de base de datos. Para obtener más información, consulte [conexión a SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sql-server-sybasetosql.md) / [conexión a Azure SQL dB &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-azure-sql-db-sybasetosql.md).  
  
-   se recomiendan 4 GB de RAM.  
  
## <a name="installing-the-ssma-for-sybase-client"></a>Instalación de SSMA para el cliente de Sybase  
SSMA es una descarga Web. Para descargar la versión más reciente, consulte la [Página de descarga de SQL Server Migration Assistant](https://aka.ms/ssmaforsybase).  
  
Después de descargar la versión más reciente, debe extraer los archivos de instalación de antes de poder instalar SSMA.  
  
**Para instalar el cliente SSMA**  
  
1.  Haga doble clic en SSMA para Sybase *n*. Instale. exe, donde *n* es el número de compilación.  
  
2.  En la página de bienvenida, haga clic en **siguiente**.  
  
    Si no tiene instalados los requisitos previos, aparecerá un mensaje que indica que primero debe instalar los componentes necesarios. Asegúrese de que ha instalado todos los requisitos previos y, a continuación, vuelva a ejecutar el programa de instalación.  
  
3.  Lea el contrato de licencia para el usuario final. Si está de acuerdo, seleccione Acepto **los términos del contrato de licencia**y, a continuación, haga clic en **siguiente**.  
  
4.  En la página elegir tipo de instalación, haga clic en **típica**.  
  
5.  Haga clic en **Instalar**.  
  
> [!IMPORTANT]  
> 1.  Desinstale todas las versiones anteriores de SSMA para Sybase antes de instalar la nueva versión.  
  
La ubicación de instalación predeterminada es C:\Archivos de Programa\microsoft SQL Server Migration Assistant para Sybase.  
  
Además de los archivos de programa de SSMA, también debe instalar SSMA for Sybase Extension Pack en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obtener más información, consulte [instalación de componentes de SSMA en SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md).  
  
## <a name="see-also"></a>Consulte también  
[Instalación de componentes de SSMA en SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)  
[Migración de bases de datos de Sybase ASE a SQL Server: Azure SQL DB &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
