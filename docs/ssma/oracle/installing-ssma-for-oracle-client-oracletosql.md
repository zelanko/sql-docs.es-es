---
title: Instalación de SSMA para cliente de Oracle (OracleToSQL) | Documentos de Microsoft
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Licensing SSMA
ms.assetid: d5d4903d-e296-4bbf-8780-63674c4d62d5
caps.latest.revision: 19
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: bacc738ab794c3ce215c000ee2c6980c09722b46
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2018
ms.locfileid: "34777531"
---
# <a name="installing-ssma-for-oracle-client-oracletosql"></a>Instalación de SSMA para cliente de Oracle (OracleToSQL)
El cliente SSMA consta de los archivos de programa que llevan a cabo las siguientes tareas:  
  
-   Conéctese a una base de datos de Oracle.  
  
-   Conectarse a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
-   Convertir objetos de base de datos de Oracle para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] sintaxis.  
  
-   Cargar los objetos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
-   Migrar datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
Este tema proporciona los requisitos previos de instalación e instrucciones para la instalación de SSMA.  
  
## <a name="prerequisites"></a>Requisitos previos  
SSMA está diseñado para trabajar con Oracle 9 o versiones posteriores y todas las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
Antes de instalar SSMA, asegúrese de que el equipo cumple los requisitos siguientes:  
  
-   Windows 7 o versiones posteriores, o Windows Server 2008 o versiones posteriores.  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 o una versión posterior.  
  
-   El [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] versión 4.0 o una versión posterior. El [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] versión 4.0 está disponible en la [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] CD del producto. También puede obtener desde la [Centro para desarrolladores de .NET Framework](http://go.microsoft.com/fwlink/?LinkId=48882).  
  
-   Cliente de Oracle 9.0 o una versión posterior y conectividad con las bases de datos de Oracle que se van a migrar. La versión de cliente de Oracle debe ser la misma versión que, o una versión posterior a la versión de la base de datos de Oracle.  
  
    Puede instalar al cliente de Oracle desde el CD del producto Oracle o desde el sitio Web de Oracle. Para obtener información acerca de la conectividad, vea [conectarse a la base de datos de Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-oracle-database-oracletosql.md).  
  
-   Acceso y permisos suficientes en el equipo que hospeda la instancia de destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o base de datos de SQL de Azure donde se va a migrar datos y objetos de base de datos. Para obtener más información, consulte [conectarse a SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-sql-server-oracletosql.md).  
  
-   4 GB de RAM recomendado.  
  
## <a name="installing-the-ssma-for-oracle-client"></a>Instalación de SSMA para cliente de Oracle  
SSMA es una descarga Web. Para descargar la versión más reciente, consulte el [página de descarga de SQL Server Migration Assistant](http://aka.ms/ssmafororacle).  
  
Después de descargar la versión más reciente, debe extraer los archivos de instalación de para poder instalar SSMA.  
  
**Para instalar al cliente SSMA**  
  
1.  Haga doble clic en SSMA para Oracle *n*. Install.exe, donde *n* es el número de compilación.  
  
2.  En la página de bienvenida, haga clic en **siguiente**.  
  
    Si no tiene los requisitos previos instalados, aparecerá un mensaje que indica que primero debe instalar los componentes necesarios. Asegúrese de que ha instalado todos los requisitos previos y, a continuación, ejecute de nuevo el programa de instalación.  
  
3.  Lea el contrato de licencia de usuario final. Si los acepta, seleccione **acepto los términos del contrato de licencia**y, a continuación, haga clic en **siguiente**.  
  
4.  En la página Elegir tipo de instalación, haga clic en **típica**.  
  
5.  Haga clic en **Instalar**.  
  
> [!IMPORTANT]  
> 1.  Desinstale todas las versiones anteriores de SSMA para Oracle antes de instalar la nueva versión.  
  
La ubicación de instalación predeterminada es C:\Program Files\Microsoft SQL Server Migration Assistant para Oracle.  
  
Además de los archivos de programa SSMA, debe instalar también la SSMA para paquete de extensión de Oracle en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Para obtener más información, consulte [instalar componentes de SSMA en SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md).  
  
## <a name="see-also"></a>Vea también  
[Instalar componentes SSMA en SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md)  
[Bases de datos de migración de Oracle a SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
