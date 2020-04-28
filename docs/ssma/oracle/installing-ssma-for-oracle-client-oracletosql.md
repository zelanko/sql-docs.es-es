---
title: Instalación de SSMA para el cliente de Oracle (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Licensing SSMA
ms.assetid: d5d4903d-e296-4bbf-8780-63674c4d62d5
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: fc295e108357040617bf6bdaa1af61fada2c97ee
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68259679"
---
# <a name="installing-ssma-for-oracle-client-oracletosql"></a>Instalación de SSMA para el cliente de Oracle (OracleToSQL)
El cliente de SSMA está formado por los archivos de programa que realizan las siguientes tareas:  
  
-   Conéctese a una base de datos de Oracle.  
  
-   Conectarse a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Convertir objetos de base de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] datos de Oracle en sintaxis.  
  
-   Cargue los objetos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Migre los datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
En este tema se proporcionan los requisitos previos de instalación y las instrucciones para instalar SSMA.  
  
## <a name="prerequisites"></a>Prerrequisitos  
SSMA está diseñado para funcionar con Oracle 9 o versiones posteriores y todas las ediciones [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]de.  
  
Antes de instalar SSMA, asegúrese de que el equipo cumple los requisitos siguientes:  
  
-   Windows 7 o versiones posteriores, o Windows Server 2008 o versiones posteriores.  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)]Windows Installer 3,1 o una versión posterior.  
  
-   La [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] versión 4,0 o una versión posterior. La [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] versión 4,0 está disponible en los [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] medios del producto. También puede obtenerlo en el [Centro para desarrolladores de .NET Framework](https://go.microsoft.com/fwlink/?LinkId=48882).  
  
-   Oracle Client 9,0 o una versión posterior y la conectividad con las bases de datos de Oracle que desea migrar. La versión del cliente de Oracle debe ser la misma versión que la versión de la base de datos de Oracle, o una versión posterior.  
  
    Puede instalar el cliente de Oracle desde el medio del producto Oracle o desde el sitio web de Oracle. Para obtener información sobre la conectividad, consulte [conexión a Oracle Database &#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-oracle-database-oracletosql.md).  
  
-   Acceso y permisos suficientes en el equipo que hospeda la instancia de destino de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Azure SQL dB, donde se van a migrar los datos y los objetos de base de datos. Para obtener más información, vea [conectarse a SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-sql-server-oracletosql.md).  
  
-   se recomiendan 4 GB de RAM.  
  
## <a name="installing-the-ssma-for-oracle-client"></a>Instalación de SSMA para el cliente de Oracle  
SSMA es una descarga Web. Para descargar la versión más reciente, consulte la [Página de descarga de SQL Server Migration Assistant](https://aka.ms/ssmafororacle).  
  
Después de descargar la versión más reciente, debe extraer los archivos de instalación de antes de poder instalar SSMA.  
  
**Para instalar el cliente SSMA**  
  
1.  Haga doble clic en SSMA para Oracle *n*. Instale. exe, donde *n* es el número de compilación.  
  
2.  En la página de bienvenida, haga clic en **Siguiente**.  
  
    Si no tiene instalados los requisitos previos, aparecerá un mensaje que indica que primero debe instalar los componentes necesarios. Asegúrese de que ha instalado todos los requisitos previos y, a continuación, vuelva a ejecutar el programa de instalación.  
  
3.  Lea el contrato de licencia para el usuario final. Si está de acuerdo, seleccione Acepto **los términos del contrato de licencia**y, a continuación, haga clic en **siguiente**.  
  
4.  En la página elegir tipo de instalación, haga clic en **típica**.  
  
5.  Haga clic en **Instalar**.  
  
> [!IMPORTANT]  
> 1.  Desinstale todas las versiones anteriores de SSMA para Oracle antes de instalar la nueva versión.  
  
La ubicación de instalación predeterminada es C:\Archivos de Programa\microsoft SQL Server Migration Assistant para Oracle.  
  
Además de los archivos de programa de SSMA, también debe instalar el paquete de extensión SSMA para Oracle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]en. Para obtener más información, consulte [instalación de componentes de SSMA en SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md).  
  
## <a name="see-also"></a>Consulte también  
[Instalación de componentes de SSMA en SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md)  
[Migrar bases de datos de Oracle a SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
